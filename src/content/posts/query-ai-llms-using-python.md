---
title: 'Query AI LLMs using Python'
published: 2025-08-05
draft: false
description: 'Use the OpenAI Python SDK to send prompts, stream tokens, and get structured JSON back — with copy‑pastable examples.'
tags: ['python', 'AI', 'LLM', 'openai']
---

This post will demonstrate how to query LLM APIs (in this case, OpenAI) using Python. It walks through installing the official SDK, loading your API key from environment variables, sending a basic text request, streaming tokens as they arrive, and requesting structured JSON via a schema. You’ll also see a lightweight retry pattern for transient errors and equivalent cURL calls so you can test endpoints from the command line.

## 1) Setup

Install the SDK and helpers:

```bash
pip install --upgrade openai python-dotenv
```

Create a `.env` file next to your script and add your key:

```env
OPENAI_API_KEY=sk-...your key...
```

Load it and initialize the client:

```python
from openai import OpenAI
from dotenv import load_dotenv
import os

load_dotenv()
client = OpenAI(api_key=os.getenv("OPENAI_API_KEY"))
```

> If you prefer, you can omit `api_key=` and rely on the environment variable directly; the SDK will pick it up.

---

## 2) Basic: send a prompt and get text back

```python
def summarize(text: str) -> str:
    res = client.responses.create(
        model="gpt-4.1-mini",
        input=f"Summarize in 3 bullet points:

{text}"
    )
    return res.output_text

if __name__ == "__main__":
    print(summarize("""
Astro is a content-first web framework. It ships little client-side JS by default and supports islands of interactivity.
"""))
```

**Run it:**

```bash
python app.py
```

You should see three concise bullets. Swap `gpt-4.1-mini` for another model if you like.

---

## 3) Stream tokens as they arrive (SSE)

Streaming gives users feedback immediately. The SDK provides a convenient stream context manager:

```python
def stream_answer(prompt: str):
    with client.responses.stream(
        model="gpt-4.1-mini",
        input=prompt
    ) as stream:
        # Print tokens as they come in
        for event in stream:
            if event.type == "response.output_text.delta":
                print(event.delta, end="", flush=True)

        # Wait for completion and fetch the final text (optional)
        final_text = stream.get_text()
        print("\n\n[done]\n")
        return final_text

if __name__ == "__main__":
    stream_answer("Give me 5 quick tips for writing clearer commit messages.")
```

**Tip:** In a web app, forward these deltas to the browser via Server‑Sent Events or websockets.

---

## 4) Ask for **strict JSON** (schema enforced)

When you need machine‑readable output, define a JSON schema and let the model conform to it.

```python
import json

def plan_todo(item: str):
    schema = {
        "name": "TodoItem",
        "schema": {
            "type": "object",
            "properties": {
                "title": {"type": "string"},
                "due_date": {"type": "string", "description": "ISO-8601 date or empty if none"},
                "priority": {"type": "integer", "minimum": 1, "maximum": 5}
            },
            "required": ["title", "priority"],
            "additionalProperties": False
        },
        "strict": True
    }

    res = client.responses.create(
        model="gpt-4.1-mini",
        input=f"Create a task for: {item}",
        response_format={
            "type": "json_schema",
            "json_schema": schema
        },
        temperature=0
    )

    # Get validated JSON string and load into Python
    json_text = res.output_text
    data = json.loads(json_text)
    return data

if __name__ == "__main__":
    print(plan_todo("Ship v1 of the blog theme"))
```

This will return something like:

```json
{ "title": "Ship v1 of the blog theme", "due_date": "", "priority": 3 }
```

Because `strict` is `True`, fields outside your schema are rejected.

---

## 5) Robust calls with retries (rate limits, timeouts)

Use a small wrapper with exponential backoff. The example below retries on common transient failures.

```python
import time
import httpx

def call_with_retries(make_call, attempts=5):
    for i in range(attempts):
        try:
            return make_call()
        except (httpx.ReadTimeout, httpx.ConnectTimeout) as e:
            if i == attempts - 1:
                raise
            sleep_s = 2 ** i
            print(f"Timeout, retrying in {sleep_s}s...")
            time.sleep(sleep_s)

def ask(prompt: str) -> str:
    def _do():
        res = client.responses.create(
            model="gpt-4.1-mini",
            input=prompt
        )
        return res.output_text
    return call_with_retries(_do)
```

---

## Bonus: cURL examples

If you just want to test from a shell, here are minimal cURL calls. Make sure `OPENAI_API_KEY` is set in your environment.

**Basic text generation**

```bash
curl https://api.openai.com/v1/responses   -H "Authorization: Bearer $OPENAI_API_KEY"   -H "Content-Type: application/json"   -d '{
    "model": "gpt-4.1-mini",
    "input": "Write a single-sentence summary of the benefits of unit tests."
  }'
```

**Structured JSON (same schema as above)**

```bash
curl https://api.openai.com/v1/responses   -H "Authorization: Bearer $OPENAI_API_KEY"   -H "Content-Type: application/json"   -d '{
    "model": "gpt-4.1-mini",
    "response_format": {
      "type": "json_schema",
      "json_schema": {
        "name": "TodoItem",
        "schema": {
          "type": "object",
          "properties": {
            "title": {"type": "string"},
            "due_date": {"type": "string"},
            "priority": {"type": "integer","minimum":1,"maximum":5}
          },
          "required": ["title","priority"],
          "additionalProperties": false
        },
        "strict": true
      }
    },
    "input": "Create a todo for fixing flaky tests"
  }'
```

---

## Troubleshooting

- **401/403**: Check your API key and that it’s in the environment where your code runs.
- **404**: Verify endpoint and model name.
- **429**: You’re rate‑limited; add backoff and reduce concurrency.
- **5xx**: Transient; retry with exponential backoff.
- **Invalid JSON**: Use `response_format` with a schema (as above) or set `temperature` lower.

---

## Where to go next

- Add conversation state by sending previous messages/outputs along with your new prompt.
- Stream to the browser with SSE for real‑time UX.
- Wrap the client in your own module so you can swap models later without touching the rest of your app.

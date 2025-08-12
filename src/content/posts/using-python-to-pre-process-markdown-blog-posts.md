---
title: 'Using Python to pre-process markdown blog posts'
published: 2025-08-12
draft: false
description: 'Learn how to automate blog post preparation with Python by pre-processing markdown files before publishing.'
tags: ['python', 'markdown', 'blogging', 'automation']
---

Markdown is a writer-friendly format, but when you’re running a blog at scale or just want consistency across posts, you can save a lot of time by automating the pre-processing step. In this guide, we’ll look at how Python can help you clean, format, and prepare markdown files before they ever reach your publishing platform.

## Why Pre-Process Markdown?

If you’ve ever had to manually fix headings, remove trailing spaces, or standardize front matter across dozens of files, you know it’s tedious and error-prone. Pre-processing lets you automate:

- Adding or verifying front matter
- Cleaning up whitespace and formatting
- Inserting SEO descriptions and tags
- Converting image paths or resizing images
- Running lint checks for markdown syntax

This means your blog posts are ready for publishing with minimal manual editing.

## Setting Up Your Python Environment

Start with a virtual environment so your tools and dependencies don’t interfere with other projects.

```bash
python3 -m venv env
source env/bin/activate
pip install pyyaml markdownlint-cli
```

We’re installing `PyYAML` for handling front matter and `markdownlint-cli` for syntax checks.

## Reading and Parsing Markdown with Front Matter

Markdown files often start with YAML front matter wrapped in triple dashes. Python’s `yaml` library makes it easy to parse and modify this.

```python
import yaml

def parse_markdown(file_path):
    with open(file_path, 'r', encoding='utf-8') as f:
        content = f.read()

    if content.startswith('---'):
        parts = content.split('---', 2)
        front_matter = yaml.safe_load(parts[1])
        body = parts[2].strip()
    else:
        front_matter = {}
        body = content.strip()

    return front_matter, body
```

This function splits the file into `front_matter` and `body`, so you can update either without touching the other.

## Adding Missing Metadata

You might want to ensure that every post has a `description` and `tags`. If they’re missing, you can insert defaults.

```python
def ensure_metadata(front_matter):
    if 'description' not in front_matter:
        front_matter['description'] = 'Default SEO description'
    if 'tags' not in front_matter:
        front_matter['tags'] = ['blog', 'python']
    return front_matter
```

## Running Automated Formatting

Use Python to enforce heading capitalization or convert tabs to spaces. For example, here’s a simple whitespace cleaner:

```python
def clean_body(body):
    lines = body.splitlines()
    cleaned = [line.rstrip() for line in lines]
    return "\n".join(cleaned).strip()
```

## Integrating Markdown Linting

Linting catches broken links, incorrect heading order, and other issues.

```bash
npx markdownlint-cli *.md
```

You can run this as part of your Python script using `subprocess` so it’s automatic.

## Batch Processing All Files

Finally, put it all together:

```python
import glob

for md_file in glob.glob('content/**/*.md', recursive=True):
    front_matter, body = parse_markdown(md_file)
    front_matter = ensure_metadata(front_matter)
    body = clean_body(body)

    new_content = f"---\n{yaml.dump(front_matter)}---\n\n{body}\n"
    with open(md_file, 'w', encoding='utf-8') as f:
        f.write(new_content)
```

This loops through every markdown file in `content/`, applies your rules, and writes the updated file.

## Automating Before Publish

You can hook this script into your build process. For example, if you’re using Astro or another static site generator, add it as an `npm` script:

```json
"scripts": {
    "prebuild": "python3 scripts/preprocess.py",
    "build": "astro build"
}
```

Now, every time you build the site, your markdown is clean and consistent.

## Final Thoughts

Pre-processing markdown with Python gives you control and consistency without slowing down your workflow. It’s a small step that can save hours of manual edits over time, especially when your blog grows beyond just a handful of posts.

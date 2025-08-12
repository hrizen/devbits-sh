---
title: 'Get started with Astro 5'
published: 2025-08-11
draft: false
description: 'A step-by-step guide to building your first site with Astro 5.'
tags: ['astro', 'web development', 'static sites']
---

Astro is a modern static site builder that focuses on delivering content faster by shipping less JavaScript to the browser. Version 5 introduces streamlined integrations, better island architecture, and improved developer experience.

## Why Choose Astro 5?

Astro 5 continues the philosophy of "content-first" sites. It’s ideal for blogs, documentation, and marketing pages, but flexible enough for interactive applications.

**Key benefits include:**

- Island architecture for partial hydration
- First-class Markdown and MDX support
- Seamless integration with React, Svelte, Vue, and others
- Improved build performance

## Installing Astro 5

You can create a new Astro project with:

```bash
npm create astro@latest my-site
cd my-site
npm install
npm run dev
```

The CLI will guide you through template choices and integrations.

## Project Structure

A basic Astro project includes:

- `src/pages/` for route-based content
- `src/components/` for reusable UI parts
- `public/` for static assets

Astro automatically maps `.astro` files in `src/pages/` to routes.

## Adding Content

Astro supports `.md` and `.mdx` files natively:

```markdown
---
title: 'Hello World'
---

# Welcome to Astro

This is my first post.
```

Place markdown files in `src/pages/` or within a content collection for structured metadata.

## Using Components

Astro lets you mix and match frameworks:

```astro
---
import MyButton from '../components/MyButton.jsx'
---

<MyButton>Click Me</MyButton>
```

You can also use `.astro` components for minimal JavaScript output.

## Styling Your Site

Astro supports CSS, Sass, Tailwind, and other styling options. Tailwind is a popular choice:

```bash
npm install -D tailwindcss
npx tailwindcss init
```

Integrate it with Astro via the Tailwind plugin for efficient styling.

## Deploying

Astro supports multiple deployment targets including static hosting and SSR. For static export:

```bash
npm run build
npm run preview
```

Deploy the `dist/` folder to Netlify, Vercel, or GitHub Pages.

## Tips for Success

- Use content collections to manage large numbers of posts
- Keep JavaScript minimal for faster load times
- Test locally before deploying to catch build errors

## Final Thoughts

Astro 5 is a strong choice for developers who want high performance without losing flexibility. Start small, then enhance interactivity where it’s needed.

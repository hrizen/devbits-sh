---
title: 'What is Typescript?'
published: 2025-08-03
draft: false
description: 'Learn what TypeScript is, why it was created, and how it differs from JavaScript.'
tags: ['typescript', 'javascript', 'history']
---

TypeScript is an open-source programming language developed by Microsoft. It’s a superset of JavaScript that adds static typing and other features to improve developer productivity and code maintainability.

## Origins of TypeScript

Released in 2012, TypeScript was created to address JavaScript’s limitations for building large-scale applications. As projects grew, developers found it difficult to manage complex codebases without stronger tooling and type checking.

## Key Features

### 1. Static Typing

TypeScript allows you to declare variable types, catching errors at compile time instead of runtime.

```typescript
let age: number = 30
let name: string = 'Alice'
```

### 2. Type Inference

You don’t always need to declare types — TypeScript can infer them from context.

```typescript
let count = 5 // inferred as number
```

### 3. Interfaces and Type Aliases

These allow you to define the shape of objects and enforce consistency.

```typescript
interface User {
  name: string
  age: number
}

function greet(user: User) {
  console.log(`Hello, ${user.name}`)
}
```

### 4. Better Tooling

TypeScript integrates deeply with IDEs, offering autocompletion, refactoring tools, and instant feedback.

### 5. Compatibility with JavaScript

All valid JavaScript is valid TypeScript. You can migrate code gradually.

## How TypeScript Differs from JavaScript

- **Typing**: JavaScript is dynamically typed, TypeScript adds static typing.
- **Compilation**: TypeScript must be compiled to JavaScript before running in a browser.
- **Tooling**: TypeScript offers stronger editor support out of the box.

## Setting Up TypeScript

Install globally:

```bash
npm install -g typescript
```

Compile a file:

```bash
tsc hello.ts
```

This generates `hello.js` which can run in any JavaScript environment.

## Why Use TypeScript?

- **Fewer runtime errors**: Catch mistakes before code runs.
- **Maintainability**: Easier to refactor and scale.
- **Clarity**: Types make the codebase more self-documenting.

## Common Use Cases

- Large enterprise applications
- Codebases with multiple contributors
- Projects requiring long-term maintenance

## Criticism

- **Extra compilation step**: Some see it as added complexity.
- **Learning curve**: Beginners must understand both JavaScript and TypeScript syntax.
- **Overhead**: For small scripts, it may be unnecessary.

## Final Thoughts

TypeScript bridges the gap between JavaScript’s flexibility and the structure of statically typed languages. For large or growing projects, it can dramatically improve reliability and developer experience.

---
title: 'Typescript Fundamentals Cheatsheet'
published: 2025-08-02
draft: false
description: 'A quick reference guide to TypeScript basics, syntax, and features.'
tags: ['typescript', 'cheatsheet', 'programming']
---

TypeScript is a strongly-typed superset of JavaScript that compiles to plain JavaScript. This cheatsheet covers the most important syntax and features you need to get started.

## Basic Types

```typescript
let isDone: boolean = false
let age: number = 42
let firstName: string = 'Alice'
let list: number[] = [1, 2, 3]
let tuple: [string, number] = ['hello', 10]
```

## Any and Unknown

```typescript
let notSure: any = 4
notSure = 'maybe a string'

let value: unknown = 'Hello'
if (typeof value === 'string') {
  console.log(value.toUpperCase())
}
```

## Functions

```typescript
function add(x: number, y: number): number {
  return x + y
}

const greet = (name: string): void => {
  console.log(`Hello, ${name}`)
}
```

## Interfaces

```typescript
interface User {
  name: string
  age?: number // optional
}

const user: User = { name: 'Bob' }
```

## Type Aliases

```typescript
type ID = string | number
let userId: ID = 123
```

## Enums

```typescript
enum Direction {
  Up,
  Down,
  Left,
  Right,
}

let dir: Direction = Direction.Up
```

## Generics

```typescript
function identity<T>(arg: T): T {
  return arg
}

let output = identity<string>('Hello')
```

## Classes

```typescript
class Person {
  constructor(
    public name: string,
    private age: number,
  ) {}

  greet() {
    console.log(`Hi, I'm ${this.name}`)
  }
}

const alice = new Person('Alice', 30)
alice.greet()
```

## Modules

```typescript
// file: math.ts
export function add(a: number, b: number): number {
  return a + b
}

// file: app.ts
import { add } from './math'
console.log(add(2, 3))
```

## Type Assertions

```typescript
let someValue: unknown = 'this is a string'
let strLength: number = (someValue as string).length
```

## Utility Types

- `Partial<T>` — all properties optional
- `Readonly<T>` — all properties read-only
- `Pick<T, K>` — select specific properties
- `Omit<T, K>` — remove specific properties

Example:

```typescript
interface Todo {
  title: string
  description: string
}

type TodoPreview = Pick<Todo, 'title'>
```

## Compilation

```bash
tsc file.ts
```

Compile and watch for changes:

```bash
tsc -w
```

## Final Thoughts

This cheatsheet gives you the essentials for working productively with TypeScript. Master these fundamentals before moving on to advanced typing and complex generics.

---
title: 'Get started with Go'
published: 2025-08-09
draft: false
description: 'Learn the basics of programming in Go and set up your development environment.'
tags: ['go', 'programming', 'getting started']
---

Go is a powerful yet simple language for building fast, reliable software. This guide walks you through installing Go, writing your first program, and understanding the basics.

## Installing Go

Go is available for Linux, macOS, and Windows. Download it from the official site:

[https://go.dev/dl/](https://go.dev/dl/)

Follow the installer prompts or extract the archive to a directory in your `PATH`.

Verify the installation:

```bash
go version
```

## Setting Up Your Workspace

Go uses a workspace model:

- **GOPATH** — Your workspace root (default: `~/go`)
- **bin** — Compiled executables
- **pkg** — Compiled package objects
- **src** — Your source code

From Go 1.18 onward, modules are the default for dependency management.

## Writing Your First Program

Create a directory for your project:

```bash
mkdir hello-go
cd hello-go
go mod init example.com/hello-go
```

Create a `main.go` file:

```go
package main

import "fmt"

func main() {
    fmt.Println("Hello, Go!")
}
```

Run it:

```bash
go run main.go
```

## Building an Executable

You can compile your program to a binary:

```bash
go build
./hello-go
```

This creates an executable named after your module.

## Understanding Go Syntax Basics

- **Packages**: Every Go program is made of packages. `main` is special—it defines an executable program.
- **Imports**: Use `import` to include packages.
- **Functions**: Declared with `func`. The `main` function is the entry point.
- **Variables**: Declared with `var` or `:=` for short form.

Example:

```go
package main

import "fmt"

func main() {
    var name string = "Alice"
    age := 30
    fmt.Printf("%s is %d years old\n", name, age)
}
```

## Go Modules and Dependencies

Add a dependency:

```bash
go get github.com/google/uuid
```

Use it in your code:

```go
package main

import (
    "fmt"
    "github.com/google/uuid"
)

func main() {
    id := uuid.New()
    fmt.Println(id)
}
```

## Next Steps

- Learn about **goroutines** for concurrency
- Explore the **standard library**
- Practice with small projects like CLI tools or APIs

## Final Thoughts

Go is easy to pick up yet capable of handling large-scale projects. With fast compilation and a rich standard library, you can go from idea to production quickly.

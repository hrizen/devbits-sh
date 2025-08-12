---
title: 'Go Cheatsheet'
published: 2025-08-08
draft: false
description: 'A quick reference guide to Go syntax, commands, and best practices.'
tags: ['go', 'cheatsheet', 'programming']
---

This cheatsheet gives you a quick reference to Go’s syntax, tools, and best practices. Keep it handy while coding.

## Basics

**Hello World:**

```go
package main

import "fmt"

func main() {
    fmt.Println("Hello, World!")
}
```

**Variables:**

```go
var name string = "Alice"
age := 30 // shorthand, type inferred
```

**Constants:**

```go
const Pi = 3.14
```

**Functions:**

```go
func add(a int, b int) int {
    return a + b
}
```

## Data Types

- `string`, `int`, `float64`, `bool`
- Arrays: `[3]int{1, 2, 3}`
- Slices: `[]int{1, 2, 3}`
- Maps: `map[string]int{"Alice": 30}`
- Structs:

```go
type Person struct {
    Name string
    Age  int
}
```

## Control Structures

**If/Else:**

```go
if x > 0 {
    fmt.Println("Positive")
} else {
    fmt.Println("Non-positive")
}
```

**Switch:**

```go
switch day {
case "Monday":
    fmt.Println("Start of week")
default:
    fmt.Println("Other day")
}
```

**For loops:**

```go
for i := 0; i < 5; i++ {
    fmt.Println(i)
}
```

## Pointers

```go
x := 10
p := &x
fmt.Println(*p) // dereference
```

## Concurrency

**Goroutines:**

```go
go func() {
    fmt.Println("Hello from a goroutine")
}()
```

**Channels:**

```go
ch := make(chan int)
go func() { ch <- 42 }()
fmt.Println(<-ch)
```

## Error Handling

```go
data, err := os.ReadFile("file.txt")
if err != nil {
    log.Fatal(err)
}
```

## Testing

Create `example_test.go`:

```go
package main

import "testing"

func TestAdd(t *testing.T) {
    if add(2, 3) != 5 {
        t.Error("Expected 5")
    }
}
```

Run tests:

```bash
go test
```

## Tooling Commands

- `go run file.go` — Run a program
- `go build` — Compile to binary
- `go test` — Run tests
- `go fmt` — Format code
- `go get` — Fetch dependencies
- `go mod init <module>` — Create a module

## Best Practices

- Keep functions short and focused
- Use `gofmt` to ensure consistent style
- Handle errors explicitly
- Prefer composition over inheritance
- Keep your `main` package minimal

## Final Thoughts

Go’s simplicity makes it easy to remember the basics, but this cheatsheet is a great quick refresher when you need it.

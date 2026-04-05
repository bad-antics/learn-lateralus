# Chapter 1: Basics

> Variables, types, functions, and printing.

## Your First Program

```lateralus
print("Hello, Lateralus!")
```

That's it. No boilerplate, no main function required for scripts.

## Variables

Use `let` for immutable bindings and `mut` for mutable ones:

```lateralus
let name = "Lateralus"       // immutable — can't reassign
mut counter = 0               // mutable — can reassign
counter += 1                  // ✓ works
// name = "other"             // ✗ compile error
```

**Rule of thumb:** Default to `let`. Use `mut` only when you need to change a value.

## Types

Lateralus has type inference, but you can be explicit:

```lateralus
let age: int = 25
let pi: float = 3.14159
let name: string = "Alice"
let active: bool = true
let scores: [int] = [90, 85, 77]
let nothing: none = none
```

| Type | Examples | Notes |
|------|----------|-------|
| `int` | `42`, `-7`, `0xFF` | 64-bit integer |
| `float` | `3.14`, `-0.5` | 64-bit floating point |
| `string` | `"hello"`, `"line\n"` | UTF-8, interpolation with `${}` |
| `bool` | `true`, `false` | |
| `[T]` | `[1, 2, 3]` | Array of type T |
| `none` | `none` | Absence of value |

## String Interpolation

Use `${}` inside double-quoted strings:

```lateralus
let name = "World"
let count = 42
print("Hello, ${name}! You have ${count} items.")
print("Math: ${2 + 2}")      // "Math: 4"
print("Upper: ${name.upper()}")  // "Upper: WORLD"
```

## Functions

```lateralus
fn add(a: int, b: int) -> int {
    a + b    // last expression is the return value
}

fn greet(name: string) -> string {
    "Hello, ${name}!"
}

print(add(3, 4))        // 7
print(greet("Alice"))   // Hello, Alice!
```

Key points:
- Parameters need type annotations
- Return type after `->`
- The last expression is implicitly returned (no `return` needed)
- You *can* use `return` for early exits

## Multiple Return with Tuples

```lateralus
fn divide(a: float, b: float) -> (float, float) {
    let quotient = a / b
    let remainder = a % b
    (quotient, remainder)
}

let (q, r) = divide(17.0, 5.0)
print("${q} remainder ${r}")   // 3.4 remainder 2.0
```

## Comments

```lateralus
// Single line comment

/// Documentation comment — shows up in tooling
/// Supports **markdown** formatting
fn documented_function() {
    // ...
}
```

---

**Exercise:** Try [exercises/01-hello.ltl](../exercises/01-hello.ltl)

**Next:** [Chapter 2 — Control Flow →](02-control-flow.md)

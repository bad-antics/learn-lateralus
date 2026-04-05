# Chapter 3: Pipelines

> The `|>` operator — Lateralus's signature feature.

## What Is a Pipeline?

The pipeline operator `|>` takes the result of the left side and passes it as the first argument to the right side:

```lateralus
// Without pipeline
let result = take(sort(filter(data, is_valid)), 10)

// With pipeline — reads top to bottom, left to right
let result = data
    |> filter(is_valid)
    |> sort()
    |> take(10)
```

Same result, dramatically more readable.

## Basic Usage

```lateralus
let message = "  Hello, World!  "
    |> trim()
    |> upper()
    |> replace("WORLD", "LATERALUS")

print(message)  // "HELLO, LATERALUS!"
```

The value flows through each step:
1. `"  Hello, World!  "` → `trim()` → `"Hello, World!"`
2. → `upper()` → `"HELLO, WORLD!"`
3. → `replace("WORLD", "LATERALUS")` → `"HELLO, LATERALUS!"`

## Pipelines with Closures

Pipelines shine with collection operations:

```lateralus
let top_scores = students
    |> filter(s => s.grade != "F")
    |> map(s => {
        name: s.name,
        percent: (s.score / s.total * 100).round(1)
    })
    |> sort_by(.percent, :desc)
    |> take(5)
```

## Building Data Transformations

```lateralus
fn process_log(raw_lines: [string]) -> [LogEntry] {
    raw_lines
        |> filter(line => !line.starts_with("#"))   // skip comments
        |> map(parse_log_entry)                      // parse each line
        |> filter(entry => entry.level != "DEBUG")   // drop debug
        |> sort_by(.timestamp)                       // chronological order
        |> dedup_by(.message)                        // remove duplicates
}
```

## Chaining with Custom Functions

Any function works in a pipeline — the piped value becomes the first argument:

```lateralus
fn double(n: int) -> int { n * 2 }
fn add(n: int, x: int) -> int { n + x }

let result = 5
    |> double()     // double(5)  → 10
    |> add(3)       // add(10, 3) → 13
    |> double()     // double(13) → 26

assert_eq(result, 26)
```

## Pipeline Assignment

You can use `|>=` to pipe-and-reassign:

```lateralus
mut items = [3, 1, 4, 1, 5, 9]
items |>= sort()
items |>= dedup()
// items is now [1, 3, 4, 5, 9]
```

## Real-World Example

```lateralus
// HTTP API response processing
fn get_active_users(response: Response) -> [UserSummary] {
    response.body
        |> json::parse()
        |> get("data.users")
        |> filter(u => u.active && u.verified)
        |> map(u => UserSummary {
            id: u.id,
            name: "${u.first} ${u.last}",
            since: u.created_at |> date::parse() |> date::relative()
        })
        |> sort_by(.name)
}
```

---

**Exercise:** Try [exercises/03-pipeline.ltl](../exercises/03-pipeline.ltl)

**Next:** [Chapter 4 — Structs & Enums →](04-structs-enums.md)

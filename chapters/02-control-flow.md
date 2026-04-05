# Chapter 2: Control Flow

> If/else, match expressions, and loops.

## If / Else

If/else is an **expression** in Lateralus — it returns a value:

```lateralus
let status = if score >= 90 {
    "excellent"
} else if score >= 70 {
    "passing"
} else {
    "needs work"
}
```

## Match Expressions

`match` is one of Lateralus's most powerful features. Think of it as a supercharged switch:

```lateralus
let message = match status_code {
    200 => "OK",
    301 => "Moved",
    404 => "Not Found",
    500 => "Server Error",
    code if code >= 400 => "Client Error (${code})",
    _   => "Unknown"
}
```

### Matching Multiple Patterns

```lateralus
match day {
    "Saturday" | "Sunday" => "Weekend! 🎉",
    _ => "Weekday 😤"
}
```

### Matching Ranges

```lateralus
match temperature {
    ..0       => "freezing",
    0..=15    => "cold",
    16..=25   => "comfortable",
    26..=35   => "warm",
    36..      => "hot"
}
```

### Match with Guards

```lateralus
match user {
    { role: "admin" }                    => grant_all(),
    { role: "user", verified: true }     => grant_basic(),
    { role: "user", verified: false }    => request_verification(),
    _                                    => deny()
}
```

## Loops

### For Loops

```lateralus
// Iterate over arrays
for item in items {
    print(item)
}

// With index
for (i, item) in items.enumerate() {
    print("${i}: ${item}")
}

// Range-based
for i in 0..10 {
    print(i)     // 0, 1, 2, ..., 9
}

for i in 0..=10 {
    print(i)     // 0, 1, 2, ..., 10 (inclusive)
}
```

### While Loops

```lateralus
mut n = 1
while n <= 100 {
    print(n)
    n *= 2
}
```

### Loop (Infinite)

```lateralus
mut tries = 0
let result = loop {
    tries += 1
    match try_connect() {
        Ok(conn) => break conn,     // break with a value
        Err(_) if tries >= 3 => break none,
        Err(_) => continue
    }
}
```

### Loop as Expression

Like `if` and `match`, loops can return values via `break`:

```lateralus
let first_even = loop {
    let n = next_random()
    if n % 2 == 0 {
        break n
    }
}
```

---

**Exercise:** Try [exercises/02-fizzbuzz.ltl](../exercises/02-fizzbuzz.ltl)

**Next:** [Chapter 3 — Pipelines →](03-pipelines.md)

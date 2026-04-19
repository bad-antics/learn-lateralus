# Chapter 11 — Error Handling

Lateralus uses result types and the `?` operator for ergonomic error handling.

## The Result type

```lateralus
fn divide(a: float, b: float) -> Result<float, string> {
    if b == 0.0 { err("division by zero") }
    else        { ok(a / b) }
}
```

## The ? operator

```lateralus
fn compute(x: float, y: float, z: float) -> Result<float, string> {
    let a = divide(x, y)?
    let b = divide(a, z)?
    ok(b + 1.0)
}
```

## Chaining with map / and_then

```lateralus
let result = divide(10.0, 2.0)
    .and_then(v => divide(v, 0.5))
    .map(v => v * 100.0)
```

## Custom error types

```lateralus
enum AppError {
    ParseError(string),
    NetworkError(int, string),
    NotFound(string),
}

fn load(path: string) -> Result<string, AppError> {
    fs.read(path).map_err(e => AppError.NotFound(path))
}
```

## Converting Option to Result

```lateralus
fn first_user(users: [User]) -> Result<User, string> {
    users.first().ok_or("no users found")
}
```

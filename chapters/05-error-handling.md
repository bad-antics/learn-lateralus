# Chapter 5: Error Handling

> Result types, try/recover, and robust code.

## The Result Type

Lateralus uses `Result<T, E>` instead of exceptions:

```lateralus
fn parse_int(s: string) -> Result<int, string> {
    match s.to_int() {
        Some(n) => Ok(n),
        None    => Err("not a valid integer: '${s}'")
    }
}

let result = parse_int("42")
match result {
    Ok(n)  => print("Got: ${n}"),
    Err(e) => print("Error: ${e}")
}
```

## Try / Recover

`try` and `recover` give you clean error handling without deep nesting:

```lateralus
fn load_config(path: string) -> Result<Config, string> {
    try {
        let text = fs::read(path)?          // ? propagates errors
        let data = json::parse(text)?
        let config = Config::from(data)?
        config
    } recover err {
        Err("Failed to load ${path}: ${err}")
    }
}
```

The `?` operator:
- If the result is `Ok(value)`, it unwraps to `value`
- If the result is `Err(e)`, it jumps to the `recover` block

## Chaining Results with Pipelines

```lateralus
fn process_input(raw: string) -> Result<Output, string> {
    raw
        |> validate()?
        |> parse()?
        |> transform()?
        |> Ok()
}
```

## The Ensure Block

`ensure` runs cleanup code whether or not an error occurred:

```lateralus
fn with_database(url: string) -> Result<Data, string> {
    let conn = db::connect(url)?

    try {
        let data = conn.query("SELECT * FROM users")?
        Ok(data)
    } recover err {
        Err("query failed: ${err}")
    } ensure {
        conn.close()     // always runs
    }
}
```

## Custom Error Types

```lateralus
enum AppError {
    NotFound(string),
    Unauthorized,
    Validation(string),
    Internal(string),
}

impl AppError {
    fn message(self) -> string {
        match self {
            AppError::NotFound(what) => "${what} not found",
            AppError::Unauthorized   => "unauthorized access",
            AppError::Validation(msg)=> "validation error: ${msg}",
            AppError::Internal(msg)  => "internal error: ${msg}",
        }
    }

    fn status_code(self) -> int {
        match self {
            AppError::NotFound(_)    => 404,
            AppError::Unauthorized   => 401,
            AppError::Validation(_)  => 422,
            AppError::Internal(_)    => 500,
        }
    }
}
```

## Providing Defaults

```lateralus
// Unwrap with a default
let port = env::get("PORT")
    |> parse_int()
    |> unwrap_or(8080)

// Unwrap with a computed default
let config = load_config("config.json")
    |> unwrap_or_else(|| Config::default())
```

---

**Exercise:** Try [exercises/05-parser.ltl](../exercises/05-parser.ltl)

**Next:** [Chapter 6 — Collections & Closures →](06-collections-closures.md)

# Chapter 13 — Macros

Lateralus macros are compile-time code generators invoked with `!`.

## Declarative macros

```lateralus
macro vec![items*] {
    {
        mut _v = []
        $(  _v.push($items)  )*
        _v
    }
}

let xs = vec![1, 2, 3]
```

## Logging macro

```lateralus
macro log!(level, msg) {
    if env.log_level() >= $level {
        eprintln("[${$level}] ${file!()}:${line!()} — ${$msg}")
    }
}
```

## derive macros

Attach behaviour to structs at compile time:

```lateralus
#[derive(Debug, Clone, PartialEq, Serialize, Deserialize)]
struct Point { x: float, y: float }
```

## Compile-time assertions

```lateralus
static_assert!(size_of<u32>() == 4, "u32 must be 4 bytes")
```

## When to use macros

- Eliminating repetitive boilerplate that can't be abstracted with functions
- Implementing DSLs (e.g. HTML builders, SQL query builders)
- Generating test tables from concise input

Prefer functions over macros whenever possible.

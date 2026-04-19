# Chapter 14 — Modules & Packages

Lateralus organises code into modules using `mod`, `use`, and `pub`.

## Declaring modules

```lateralus
// src/math.ltl
pub fn add(a: int, b: int) -> int { a + b }
pub fn sub(a: int, b: int) -> int { a - b }
```

```lateralus
// main.ltl
use math.{add, sub}
print(add(3, 4))
```

## Nested modules

```lateralus
mod utils {
    pub mod string {
        pub fn capitalise(s: string) -> string {
            s[0..1].to_uppercase() + s[1..]
        }
    }
}

use utils.string.capitalise
print(capitalise("hello"))
```

## Re-exporting

```lateralus
mod prelude {
    pub use math.{add, sub}
    pub use utils.string.capitalise
}
```

## Package layout

```
my_project/
  lateralus.toml
  src/
    main.ltl
    lib.ltl
    math/
      mod.ltl
      algebra.ltl
      geometry.ltl
  tests/
    integration.ltl
```

## lateralus.toml

```toml
[package]
name    = "my_project"
version = "0.1.0"

[dependencies]
http = "1.2"
json = "2.0"
```

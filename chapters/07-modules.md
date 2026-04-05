# Chapter 7: Modules & Imports

> Organize code into files and expose public APIs.

## File = Module

Every `.ltl` file is a module. The filename becomes the module name:

```
my-project/
├── src/
│   ├── main.ltl        ← entry point
│   ├── math.ltl        ← module "math"
│   └── utils/
│       ├── strings.ltl ← module "utils/strings"
│       └── dates.ltl   ← module "utils/dates"
```

## Imports

```lateralus
// Import specific items
import { add, multiply } from "./math"

// Import everything
import * from "./math"

// Import with alias
import { Connection as Conn } from "./db"

// Import a module as a namespace
import math from "./math"
math.add(1, 2)
```

## Pub — Public API

By default, everything is private to its module. Use `pub` to export:

```lateralus
// math.ltl

// Public — other modules can use these
pub fn add(a: int, b: int) -> int { a + b }
pub fn multiply(a: int, b: int) -> int { a * b }

pub struct Vector {
    pub x: float,    // public field
    pub y: float,
    magnitude: float, // private field
}

// Private — only this module can use this
fn internal_helper() {
    // ...
}
```

## Organizing Larger Projects

```
project/
├── lateralus.toml
├── src/
│   ├── main.ltl
│   ├── config.ltl
│   ├── routes/
│   │   ├── mod.ltl        ← re-exports from this folder
│   │   ├── users.ltl
│   │   └── posts.ltl
│   ├── models/
│   │   ├── mod.ltl
│   │   ├── user.ltl
│   │   └── post.ltl
│   └── services/
│       ├── mod.ltl
│       ├── auth.ltl
│       └── email.ltl
```

### Re-Exporting with mod.ltl

```lateralus
// routes/mod.ltl — barrel file
pub import { user_routes } from "./users"
pub import { post_routes } from "./posts"
```

```lateralus
// main.ltl — clean imports
import { user_routes, post_routes } from "./routes"
```

## The lateralus.toml File

```toml
[project]
name = "my-app"
version = "1.0.0"
entry = "src/main.ltl"

[dependencies]
http = "0.3.0"
json = "1.2.0"

[dev-dependencies]
mock = "0.1.0"
```

---

**Exercise:** Try [exercises/07-library.ltl](../exercises/07-library.ltl)

**Next:** [Chapter 8 — Your First Project →](08-first-project.md)

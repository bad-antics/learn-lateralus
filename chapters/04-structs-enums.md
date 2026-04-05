# Chapter 4: Structs & Enums

> Custom types, impl blocks, and methods.

## Structs

Structs group related data together:

```lateralus
struct Point {
    x: float,
    y: float,
}

let origin = Point { x: 0.0, y: 0.0 }
let p = Point { x: 3.0, y: 4.0 }
print("x = ${p.x}")  // x = 3.0
```

## Impl Blocks

Add methods to your structs with `impl`:

```lateralus
struct Point {
    x: float,
    y: float,
}

impl Point {
    // Constructor
    fn new(x: float, y: float) -> Point {
        Point { x, y }     // shorthand when field name == variable name
    }

    // Instance method (takes self)
    fn distance_to(self, other: Point) -> float {
        let dx = self.x - other.x
        let dy = self.y - other.y
        (dx * dx + dy * dy).sqrt()
    }

    // Returns a new Point (immutable style)
    fn translate(self, dx: float, dy: float) -> Point {
        Point { x: self.x + dx, y: self.y + dy }
    }

    fn display(self) -> string {
        "(${self.x}, ${self.y})"
    }
}

let a = Point::new(0.0, 0.0)
let b = Point::new(3.0, 4.0)
print(a.distance_to(b))   // 5.0
print(b.translate(1.0, -1.0).display())  // (4.0, 3.0)
```

## Enums

Enums define a type with a fixed set of variants:

```lateralus
enum Direction {
    North,
    South,
    East,
    West,
}

fn describe(dir: Direction) -> string {
    match dir {
        Direction::North => "heading north",
        Direction::South => "heading south",
        Direction::East  => "heading east",
        Direction::West  => "heading west",
    }
}
```

### Enums with Data

Variants can hold data:

```lateralus
enum Shape {
    Circle(float),                    // radius
    Rectangle(float, float),          // width, height
    Triangle(float, float, float),    // three sides
}

impl Shape {
    fn area(self) -> float {
        match self {
            Shape::Circle(r) => 3.14159 * r * r,
            Shape::Rectangle(w, h) => w * h,
            Shape::Triangle(a, b, c) => {
                let s = (a + b + c) / 2.0
                (s * (s - a) * (s - b) * (s - c)).sqrt()
            }
        }
    }

    fn describe(self) -> string {
        match self {
            Shape::Circle(r)       => "circle (r=${r})",
            Shape::Rectangle(w, h) => "rectangle (${w}×${h})",
            Shape::Triangle(..)    => "triangle",
        }
    }
}

let shapes = [
    Shape::Circle(5.0),
    Shape::Rectangle(3.0, 4.0),
    Shape::Circle(1.0),
]

// Pipelines + enums = ❤️
let total_area = shapes
    |> map(s => s.area())
    |> sum()

print("Total area: ${total_area:.2}")
```

## Struct Update Syntax

Create a modified copy with `...`:

```lateralus
struct Config {
    host: string,
    port: int,
    debug: bool,
    timeout: int,
}

let default = Config { host: "localhost", port: 8080, debug: false, timeout: 30 }
let dev = Config { debug: true, port: 3000, ...default }
// dev has debug=true, port=3000, host="localhost", timeout=30
```

---

**Exercise:** Try [exercises/04-shapes.ltl](../exercises/04-shapes.ltl)

**Next:** [Chapter 5 — Error Handling →](05-error-handling.md)

# Chapter 6: Collections & Closures

> Arrays, maps, and higher-order functions.

## Arrays

```lateralus
let numbers = [1, 2, 3, 4, 5]
let names = ["Alice", "Bob", "Charlie"]
let empty: [int] = []

// Access
print(numbers[0])        // 1
print(numbers.len())     // 5
print(numbers.last())    // Some(5)

// Slicing
print(numbers[1..3])     // [2, 3]
print(numbers[2..])      // [3, 4, 5]
```

### Array Methods

```lateralus
let items = [3, 1, 4, 1, 5, 9, 2, 6]

items.contains(5)          // true
items.index_of(4)          // Some(2)
items.reverse()            // [6, 2, 9, 5, 1, 4, 1, 3]
items.sort()               // [1, 1, 2, 3, 4, 5, 6, 9]
items.dedup()              // [1, 2, 3, 4, 5, 6, 9]
items.chunks(3)            // [[3, 1, 4], [1, 5, 9], [2, 6]]
items.flatten()            // flattens nested arrays
items.zip(other)           // pairs elements
```

## Maps

```lateralus
let scores = {
    "Alice": 95,
    "Bob": 82,
    "Charlie": 91,
}

// Access
print(scores["Alice"])        // 95
print(scores.get("Dave"))     // None
print(scores.get_or("Dave", 0))  // 0

// Iterate
for (name, score) in scores {
    print("${name}: ${score}")
}

// Map methods
scores.keys()      // ["Alice", "Bob", "Charlie"]
scores.values()    // [95, 82, 91]
scores.len()       // 3
scores.has("Bob")  // true
```

## Closures

Closures are anonymous functions that capture their environment:

```lateralus
// Short form
let double = x => x * 2
let add = (a, b) => a + b

// Block form
let process = (item) => {
    let cleaned = item.trim().lower()
    let validated = validate(cleaned)
    validated
}
```

## Higher-Order Functions

Functions that take or return other functions:

```lateralus
// filter — keep items that match
[1, 2, 3, 4, 5] |> filter(n => n > 3)    // [4, 5]

// map — transform each item
[1, 2, 3] |> map(n => n * 10)             // [10, 20, 30]

// reduce — combine into single value
[1, 2, 3, 4] |> reduce(0, (acc, n) => acc + n)   // 10

// each — side effects (returns nothing)
items |> each(item => print(item))

// find — first match
[1, 2, 3, 4] |> find(n => n > 2)          // Some(3)

// any / all — boolean checks
[1, 2, 3] |> any(n => n > 2)              // true
[1, 2, 3] |> all(n => n > 0)              // true

// group_by — partition into map
users |> group_by(.role)
// { "admin": [...], "user": [...] }

// flat_map — map + flatten
[[1, 2], [3, 4]] |> flat_map(arr => arr)   // [1, 2, 3, 4]
```

## Combining Everything

```lateralus
struct Sale {
    product: string,
    amount: float,
    region: string,
}

fn regional_report(sales: [Sale]) -> {string: float} {
    sales
        |> filter(s => s.amount > 0.0)
        |> group_by(.region)
        |> map_values(group => {
            group
                |> map(.amount)
                |> sum()
        })
}

// Usage
let report = sales |> regional_report()
for (region, total) in report |> sort_by_value(:desc) {
    print("${region}: $${total:.2}")
}
```

## Returning Functions

```lateralus
fn make_multiplier(factor: int) -> fn(int) -> int {
    n => n * factor
}

let triple = make_multiplier(3)
print(triple(7))     // 21

// Useful in pipelines
[1, 2, 3, 4, 5]
    |> map(make_multiplier(10))   // [10, 20, 30, 40, 50]
```

---

**Exercise:** Try [exercises/06-wordcount.ltl](../exercises/06-wordcount.ltl)

**Next:** [Chapter 7 — Modules & Imports →](07-modules.md)

# Chapter 10 — Generics & Traits

Lateralus supports full parametric polymorphism through generics and
compile-time trait bounds.

## Generic functions

```lateralus
fn first<T>(list: [T]) -> T? {
    list.get(0)
}
```

## Trait bounds

```lateralus
fn max_item<T: Ord>(items: [T]) -> T? {
    items |> fold(none, |acc, x| match acc {
        none    => some(x),
        some(m) => some(if x > m { x } else { m }),
    })
}
```

## Generic structs

```lateralus
struct Stack<T> {
    items: [T],
}

impl<T> Stack<T> {
    fn push(mut self, v: T) { self.items.push(v) }
    fn pop(mut self) -> T?  { self.items.pop() }
    fn peek(self) -> T?     { self.items.last() }
}
```

## Multiple bounds

```lateralus
fn sorted_dedup<T: Ord + Hash>(items: [T]) -> [T] {
    items |> sort() |> dedup()
}
```

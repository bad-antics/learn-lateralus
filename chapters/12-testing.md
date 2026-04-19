# Chapter 12 — Testing

Lateralus has first-class testing support via the `test` block.

## Unit tests

```lateralus
test "addition works" {
    assert_eq(1 + 1, 2)
    assert_eq(2 + 2, 4)
}
```

## Table-driven tests

```lateralus
test "is_even table" {
    let cases = [(2, true), (3, false), (0, true), (-4, true)]
    for (n, expected) in cases {
        assert_eq(n % 2 == 0, expected, "n=${n}")
    }
}
```

## Setup and teardown

```lateralus
test_suite "Database" {
    mut db: DB

    setup { db = DB.open(":memory:") }
    teardown { db.close() }

    test "insert and select" {
        db.execute("INSERT INTO t VALUES (1, 'hello')")
        let rows = db.query("SELECT * FROM t")
        assert_eq(rows.len(), 1)
    }
}
```

## Property-based tests

```lateralus
test_prop "sort is idempotent" forall xs: [int] {
    let once  = xs.sort()
    let twice = once.sort()
    assert_eq(once, twice)
}
```

## Running tests

```bash
lateralus test           # run all tests
lateralus test --filter sort  # run matching tests
```

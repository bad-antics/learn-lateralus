# Chapter 9 — Async / Await

Lateralus has built-in concurrency through `async` functions and the `await`
keyword. The runtime schedules async tasks on a lightweight thread pool.

## Declaring async functions

```lateralus
async fn fetch_json(url: string) -> dict<string, json.Value> {
    let resp = await http.get(url)
    resp.json()
}
```

## Running tasks concurrently

```lateralus
let (users, posts) = await parallel(
    fetch_json("https://api.example.com/users"),
    fetch_json("https://api.example.com/posts"),
)
```

## Timeouts and cancellation

```lateralus
let result = await fetch_json(url) |> timeout(5000)
match result {
    ok(data)  => print(data),
    err(e)    => print("Timed out: ${e}"),
}
```

## Channels

```lateralus
let (tx, rx) = channel()

spawn(async || {
    for i in range(0, 5) {
        await tx.send(i)
    }
    tx.close()
})

while let some(v) = await rx.recv() {
    print("Got: ${v}")
}
```

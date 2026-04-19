# Chapter 15 — Building a Real Project

Putting it all together: a command-line task manager.

## Project structure

```
taskr/
  lateralus.toml
  src/
    main.ltl       — CLI entry point
    db.ltl         — SQLite storage
    models.ltl     — Task struct + Status enum
    commands.ltl   — add / list / done / delete
```

## models.ltl

```lateralus
pub enum Status { Todo, InProgress, Done }

pub struct Task {
    id:         int,
    title:      string,
    status:     Status,
    created_at: DateTime,
    tags:       [string],
}
```

## commands.ltl — add

```lateralus
pub fn add(db: DB, title: string, tags: [string]) -> Result<Task, AppError> {
    let task = Task {
        id:         db.next_id(),
        title,
        status:     Status.Todo,
        created_at: DateTime.now(),
        tags,
    }
    db.insert(task)?
    ok(task)
}
```

## main.ltl — CLI wiring

```lateralus
use std.cli.{Cli, Arg}

fn main() {
    let cli = Cli.new("taskr", "1.0.0")
        .subcommand("add",    "Add a task",    [Arg.pos("title"), Arg.flag("tag", "t")])
        .subcommand("list",   "List tasks",    [Arg.flag("status", "s")])
        .subcommand("done",   "Mark done",     [Arg.pos("id")])
        .subcommand("delete", "Delete a task", [Arg.pos("id")])

    let db = DB.open(env.home() + "/.taskr.db")

    match cli.parse(env.args()) {
        ("add",    args) => commands.add(db, args["title"], args.all("tag")),
        ("list",   args) => commands.list(db, args.get("status")),
        ("done",   args) => commands.done(db, args["id"].parse_int()?),
        ("delete", args) => commands.delete(db, args["id"].parse_int()?),
        _                => { cli.help(); ok(()) },
    } .unwrap_or_else(|e| { eprintln("Error: ${e}"); process.exit(1) })
}

main()
```

## Exercises

1. Add a `due_date` field to `Task` and a `--due` flag to `add`
2. Implement a `search` subcommand that filters by title substring
3. Add coloured output: red for overdue tasks, green for Done
4. Write integration tests that exercise the full CLI via `Command.run`

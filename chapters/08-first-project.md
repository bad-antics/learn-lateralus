# Chapter 8: Your First Project

> Build something real and push it to GitHub.

You've learned the language. Now let's put it all together.

## Step 1: Create Your Project

The fastest way — use the template:

1. Go to [lateralus-quickstart](https://github.com/bad-antics/lateralus-quickstart)
2. Click **"Use this template"** → **"Create a new repository"**
3. Name it whatever you want
4. Clone it locally:

```bash
git clone https://github.com/YOUR_USERNAME/your-project.git
cd your-project
```

Or start from scratch:

```bash
mkdir my-project && cd my-project
mkdir src tests
```

## Step 2: Write Your Code

Let's build a **task tracker** — a CLI tool that manages a todo list.

Create `src/main.ltl`:

```lateralus
import { TaskStore } from "./store"
import { parse_command } from "./cli"

fn main() {
    let store = TaskStore::load("tasks.json")
        |> unwrap_or_else(|| TaskStore::new())

    let args = env::args()

    match parse_command(args) {
        Command::Add(text) => {
            store.add(text)
            store.save("tasks.json")?
            print("✓ Added: ${text}")
        },
        Command::List => {
            store.tasks
                |> enumerate()
                |> each((i, task) => {
                    let check = if task.done { "✓" } else { " " }
                    print("[${check}] ${i + 1}. ${task.text}")
                })
        },
        Command::Done(index) => {
            store.complete(index)?
            store.save("tasks.json")?
            print("✓ Marked #${index + 1} as done")
        },
        Command::Help => print_help(),
    }
}

fn print_help() {
    print("Usage:")
    print("  tasks add <text>    Add a task")
    print("  tasks list          List all tasks")
    print("  tasks done <n>      Mark task as done")
}

main()
```

Create `src/store.ltl`:

```lateralus
pub struct Task {
    pub text: string,
    pub done: bool,
}

pub struct TaskStore {
    pub tasks: [Task],
}

impl TaskStore {
    pub fn new() -> TaskStore {
        TaskStore { tasks: [] }
    }

    pub fn load(path: string) -> Result<TaskStore, string> {
        let data = fs::read(path)?
        let tasks = json::parse(data)?
        Ok(TaskStore { tasks })
    }

    pub fn save(self, path: string) -> Result<none, string> {
        let data = json::stringify(self.tasks, indent: 2)
        fs::write(path, data)
    }

    pub fn add(mut self, text: string) {
        self.tasks.push(Task { text, done: false })
    }

    pub fn complete(mut self, index: int) -> Result<none, string> {
        if index < 0 || index >= self.tasks.len() {
            return Err("invalid task index: ${index}")
        }
        self.tasks[index].done = true
        Ok(none)
    }
}
```

Create `src/cli.ltl`:

```lateralus
pub enum Command {
    Add(string),
    List,
    Done(int),
    Help,
}

pub fn parse_command(args: [string]) -> Command {
    match args[1..] {
        ["add", ...rest] => Command::Add(rest.join(" ")),
        ["list"]         => Command::List,
        ["done", n]      => {
            match n.to_int() {
                Some(i) => Command::Done(i - 1),
                None    => Command::Help
            }
        },
        _ => Command::Help
    }
}
```

## Step 3: Test It

Create `tests/test_store.ltl`:

```lateralus
import { TaskStore, Task } from "../src/store"

test "add creates a task" {
    mut store = TaskStore::new()
    store.add("learn lateralus")
    assert_eq(store.tasks.len(), 1)
    assert_eq(store.tasks[0].text, "learn lateralus")
    assert(!store.tasks[0].done)
}

test "complete marks task done" {
    mut store = TaskStore::new()
    store.add("test task")
    store.complete(0).unwrap()
    assert(store.tasks[0].done)
}

test "complete rejects invalid index" {
    let store = TaskStore::new()
    assert(store.complete(5).is_err())
}
```

Run them:

```bash
lateralus test
```

## Step 4: Push to GitHub

```bash
git add -A
git commit -m "Build task tracker in Lateralus"
git push origin main
```

🎉 **Congratulations!** You've just:
- Written a real Lateralus project
- Used pipelines, pattern matching, structs, enums, and error handling
- Pushed `.ltl` files to GitHub

## What Next?

| Goal | Resource |
|------|----------|
| See more examples | [lateralus-examples](https://github.com/bad-antics/lateralus-examples) |
| Read the full docs | [lateralus-lang](https://github.com/bad-antics/lateralus-lang) |
| Experiment online | [Playground](https://bad-antics.github.io/lateralus/playground.html) |
| Join the community | [Discussions](https://github.com/bad-antics/lateralus-lang/discussions) |

---

**← Back to [Table of Contents](../README.md)**

# 📖 Learn Lateralus

> **Go from zero to productive in 30 minutes.**

Lateralus is a modern programming language built around **pipelines**, **pattern matching**, and **expressive types**. This guide walks you through everything you need to start writing real code.

[![Try Online](https://img.shields.io/badge/playground-try%20online-7c5cfc?style=for-the-badge)](https://bad-antics.github.io/lateralus/playground.html)
[![Install](https://img.shields.io/badge/pip-install%20lateralus--lang-34d399?style=for-the-badge&logo=pypi)](https://pypi.org/project/lateralus-lang/)
[![VS Code](https://img.shields.io/badge/extension-VS%20Code-007ACC?style=for-the-badge&logo=visualstudiocode)](https://marketplace.visualstudio.com/items?itemName=lateralus.lateralus-lang)

---

## Table of Contents

| # | Chapter | What You'll Learn |
|---|---------|-------------------|
| 1 | [Basics](chapters/01-basics.md) | Variables, types, functions, printing |
| 2 | [Control Flow](chapters/02-control-flow.md) | If/else, match, loops |
| 3 | [Pipelines](chapters/03-pipelines.md) | The `\|>` operator, chaining, composition |
| 4 | [Structs & Enums](chapters/04-structs-enums.md) | Custom types, impl blocks, methods |
| 5 | [Error Handling](chapters/05-error-handling.md) | Result, try/recover, propagation |
| 6 | [Collections & Closures](chapters/06-collections-closures.md) | Arrays, maps, higher-order functions |
| 7 | [Modules & Imports](chapters/07-modules.md) | Project structure, pub, imports |
| 8 | [Your First Project](chapters/08-first-project.md) | Build something real, push to GitHub |

## How to Use This Guide

**Option A — Read online:** Click the chapters above.

**Option B — Follow along locally:**

```bash
# Install Lateralus
pip install lateralus-lang

# Clone this repo
git clone https://github.com/bad-antics/learn-lateralus.git
cd learn-lateralus

# Run any exercise
lateralus run exercises/01-hello.ltl
```

**Option C — Try in the browser:** Use the [Playground](https://bad-antics.github.io/lateralus/playground.html) — no install needed.

## Exercises

Each chapter has a matching exercise in the `exercises/` folder. Try them yourself, then check `solutions/` when you're ready.

| Exercise | File | Concepts |
|---|---|---|
| Hello Pipeline | [exercises/01-hello.ltl](exercises/01-hello.ltl) | Variables, print, functions |
| FizzBuzz | [exercises/02-fizzbuzz.ltl](exercises/02-fizzbuzz.ltl) | Match, loops, modulo |
| Data Pipeline | [exercises/03-pipeline.ltl](exercises/03-pipeline.ltl) | `\|>`, filter, map, reduce |
| Shape Calculator | [exercises/04-shapes.ltl](exercises/04-shapes.ltl) | Enums, structs, pattern matching |
| Safe Parser | [exercises/05-parser.ltl](exercises/05-parser.ltl) | Result, try/recover, error handling |
| Word Counter | [exercises/06-wordcount.ltl](exercises/06-wordcount.ltl) | Maps, closures, pipelines |
| Mini Library | [exercises/07-library.ltl](exercises/07-library.ltl) | Modules, imports, pub |
| CLI Tool | [exercises/08-cli.ltl](exercises/08-cli.ltl) | Full project, args, file I/O |

## What Next?

- 🚀 [Start a project](https://github.com/bad-antics/lateralus-quickstart) — Use the template repo
- 💡 [See examples](https://github.com/bad-antics/lateralus-examples) — Real-world code patterns
- 🎮 [Playground](https://bad-antics.github.io/lateralus/playground.html) — Experiment in the browser
- 📚 [Full docs](https://github.com/bad-antics/lateralus-lang) — Language reference
- 🧩 [VS Code Extension](https://marketplace.visualstudio.com/items?itemName=lateralus.lateralus-lang) — Editor support

## Contributing

Found a typo? Have a better explanation? **PRs welcome!** This is a community resource.

## License

MIT

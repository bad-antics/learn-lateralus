# learn-lateralus

A structured, self-paced course for learning the Lateralus programming language.
Each chapter includes a lesson (`.md`) + exercises (`.ltl`) + solutions (`.ltl`).

## Chapters

| # | Topic | Chapter | Exercise | Solution |
|---|-------|---------|----------|---------|
| 01 | Basics | [chapter](chapters/01-basics.md) | [exercise](exercises/01-basics.ltl) | [solution](solutions/01-basics.ltl) |
| 02 | Variables & Types | [chapter](chapters/02-variables-types.md) | [exercise](exercises/02-variables-types.ltl) | [solution](solutions/02-variables-types.ltl) |
| 03 | Control Flow | [chapter](chapters/03-control-flow.md) | [exercise](exercises/03-control-flow.ltl) | [solution](solutions/03-control-flow.ltl) |
| 04 | Functions | [chapter](chapters/04-functions.md) | [exercise](exercises/04-functions.ltl) | [solution](solutions/04-functions.ltl) |
| 05 | Structs & Enums | [chapter](chapters/05-structs-enums.md) | [exercise](exercises/05-structs-enums.ltl) | [solution](solutions/05-structs-enums.ltl) |
| 06 | Pipelines | [chapter](chapters/06-pipelines.md) | [exercise](exercises/06-pipelines.ltl) | [solution](solutions/06-pipelines.ltl) |
| 07 | Pattern Matching | [chapter](chapters/07-pattern-matching.md) | [exercise](exercises/07-pattern-matching.ltl) | [solution](solutions/07-pattern-matching.ltl) |
| 08 | Collections | [chapter](chapters/08-collections.md) | [exercise](exercises/08-collections.ltl) | [solution](solutions/08-collections.ltl) |
| 09 | Async / Await | [chapter](chapters/09-async-await.md) | [exercise](exercises/09-async-await.ltl) | [solution](solutions/09-async-await.ltl) |
| 10 | Generics & Traits | [chapter](chapters/10-generics.md) | [exercise](exercises/10-generics.ltl) | [solution](solutions/10-generics.ltl) |
| 11 | Error Handling | [chapter](chapters/11-error-handling.md) | [exercise](exercises/11-error-handling.ltl) | [solution](solutions/11-error-handling.ltl) |
| 12 | Testing | [chapter](chapters/12-testing.md) | [exercise](exercises/12-testing.ltl) | [solution](solutions/12-testing.ltl) |
| 13 | Macros | [chapter](chapters/13-macros.md) | [exercise](exercises/13-macros.ltl) | [solution](solutions/13-macros.ltl) |
| 14 | Modules & Packages | [chapter](chapters/14-modules.md) | [exercise](exercises/14-modules.ltl) | [solution](solutions/14-modules.ltl) |
| 15 | Real Project | [chapter](chapters/15-real-project.md) | [exercise](exercises/15-real-project.ltl) | [solution](solutions/15-real-project.ltl) |

## Getting started

```bash
# Install Lateralus
curl -fsSL https://lateralus.dev/install.sh | sh

# Run an exercise
lateralus run exercises/01-basics.ltl

# Check your solution against the reference
lateralus run solutions/01-basics.ltl
```

## Structure

```
learn-lateralus/
  chapters/    01-15.md    — Lesson text with examples
  exercises/   01-15.ltl   — Incomplete code to fill in
  solutions/   01-15.ltl   — Reference implementations
```

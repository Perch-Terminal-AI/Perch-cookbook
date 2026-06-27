# One-shot a task

**Surface:** CLI

`perch run` hands a whole task to the operator in one command. It uses the same turn runtime as the desktop app, so it can read files, run commands, search, and write output, then report back.

## Basic

```bash
perch run "research the current status of this folder and tell me what matters"
```

## Pick how it works

```bash
# Just answer, no tools
perch run "explain what this repo does" --mode ask

# Plan first, then execute as a multi-step agent run
perch run "set up a basic test harness for this project" --mode agents
```

Modes:

- `--mode ask` returns a direct answer and does not touch your files.
- `--mode agents` plans and executes a multi-step task.
- `--mode plan` produces a plan you can review before running.

## Pick a working style

```bash
perch run "write a concise status update for this folder" --mode agents --persona quill
perch run "find anything in these exports that looks wrong" --mode agents --persona saffron
```

## Control how much it can do on its own

```bash
# Review each step before it runs
perch run "refactor this module" --permission auto_review

# Let it run autonomously
perch run "build a small CLI that converts these CSVs to JSON" --permission take_the_wheel
```

## Point it at a different folder

```bash
perch run "summarize the open issues here" --cwd ~/projects/some-repo
```

## Get machine-readable output

```bash
perch run "list the files that changed most recently" --mode ask --json
```

## Notes

The CLI exposes terminal-safe local capabilities: shell, file read and write, local AP tools, sandboxed code execution, and public web research where configured. The embedded browser and desktop indexing stay on the desktop app.

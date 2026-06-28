# Perch Cookbook

Runnable recipes for [Perch](https://perchai.app), the AI operator for work you can check.

Each recipe is a small, real task with the exact commands to run it. They are grouped by surface, because some capabilities live on the desktop app and some are terminal-safe in the CLI. Where a recipe is web or desktop only, it says so.

## Install the CLI

```bash
npm install -g perchai-cli
```

Then sign in once. The CLI shares the same account, memory, and usage as the web and desktop apps.

```bash
perch run "summarize what Perch can do"
```

## Recipes

| # | Recipe | Surface | What you learn |
|---|--------|---------|----------------|
| 01 | [One-shot a task](recipes/01-one-shot-a-task.md) | CLI | Hand Perch a whole task and let it run |
| 02 | [Find duplicate payments in a folder](recipes/02-find-duplicate-payments.md) | CLI | Run an AP audit over real files |
| 03 | [Deterministic AP checks in CI](recipes/03-deterministic-checks-in-ci.md) | CLI | Assert exact financial totals in a pipeline |
| 04 | [Verify citations in a draft](recipes/04-verify-citations.md) | Web / Desktop | Catch unsupported and fabricated citations |
| 05 | [Analyze a spreadsheet with sandboxed Python](recipes/05-analyze-a-spreadsheet.md) | CLI | Profile messy data with deterministic checks |

## How Perch is different

The recipes share one idea. Perch does not ask a model to be the thing that computes the answer. The checks run as deterministic logic over your actual files, and the model reads, routes, and explains. That is why recipe 03 can assert an exact total in a CI pipeline: the number is computed, not generated, so it is the same every run.

## Two working styles

Most recipes let you pick a persona with `--persona`:

- **Saffron** reads files under pressure: audits, reconciliations, analysis.
- **Quill** writes with sources: memos, briefs, drafts.

## Contributing

Have a recipe that shows Perch doing something useful? Open a pull request with a new file in `recipes/`, following the format of the existing ones. Keep it real and runnable.

## Links

- [Website](https://perchai.app)
- [Docs](https://perchai.app/docs)
- [Try it on the web](https://chat.perchai.app)

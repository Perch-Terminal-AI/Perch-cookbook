# Analyze a spreadsheet with sandboxed Python

**Surface:** CLI

`perch run` over a messy CSV. Perch profiles the data, runs deterministic checks in a sealed sandbox, and explains what it found. The counting is done by Python; the explanation is done by the model.

## Run it

```bash
perch run "profile this spreadsheet and flag anomalies" \
  --mode agents --cwd ./examples/sales-data
```

## What Perch computes

- **Schema:** column names, inferred types, null rates
- **Duplicates:** exact duplicate rows
- **Outliers:** statistical anomalies in numeric columns
- **Consistency:** formatting irregularities (dates, currencies, IDs)
- **Coverage:** missing values by column

## Get machine-readable output

```bash
perch run "profile this spreadsheet and return the results as JSON" \
  --mode agents --cwd ./examples/sales-data --json
```

## Ask in plain language instead

If you would rather drive it conversationally, hand the folder to Saffron:

```bash
perch run "this sales data looks messy. profile it, find duplicates and outliers, and tell me what needs cleaning" \
  --mode agents --persona saffron --cwd ./examples/sales-data
```

## Why this is not a chatbot answer

The profile is computed from the data, not inferred by a model. Python runs the math in a sealed sandbox; the model reads the results and explains them. Every number comes back with the code that produced it, so a reviewer can confirm or overrule it. That is the difference between a finding you can defend and a sentence that sounds right.

## Notes

The sandbox runs in a sealed environment with no network access. Your data is copied in, analyzed, and the results are returned. The original file is never modified.

Perch uses the `run_sandbox_code` tool for this, which is available in the CLI when running with `--mode agents`. The model decides what Python to write based on the file it sees, and the sandbox executes it deterministically.

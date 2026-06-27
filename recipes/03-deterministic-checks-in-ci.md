# Deterministic AP checks in CI

**Surface:** CLI

Because the accounts payable checks are computed rather than generated, they return the same numbers every run. That means you can assert them in a pipeline, the same way you assert a unit test. `perch test ap` exists for exactly this.

## Assert exact totals

```bash
perch test ap ./examples/ap-folder \
  --expect totalSpend=699559.79 \
  --expect duplicateRecoverableExposure=94890.13
```

The command exits non-zero if any expected value does not match, so a regression in the data or the pipeline fails the build instead of slipping through.

## Run a named profile

```bash
perch test ap ./examples/ap-folder --profile financial-lab-v2 --json
```

## Wire it into GitHub Actions

```yaml
# .github/workflows/ap-check.yml
name: AP check
on: [push]
jobs:
  ap:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with:
          node-version: 20
      - run: npm install -g perchai-cli
      # Authenticate the CLI non-interactively here using your account token.
      # See https://perchai.app/docs for the current CI auth step.
      - run: |
          perch test ap ./data/ap \
            --expect totalSpend=699559.79 \
            --expect duplicateRecoverableExposure=94890.13 \
            --json
```

## Why this matters

A test you can write against a financial total is a strong signal that the underlying work is real computation, not a language model guessing. If the number can drift between runs, it was never a check. This recipe is the clearest demonstration of what Perch means by work you can verify.

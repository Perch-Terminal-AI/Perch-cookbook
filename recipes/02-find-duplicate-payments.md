# Find duplicate payments in a folder

**Surface:** CLI

`perch ap evidence` runs the accounts payable checks over a folder of real files and prepares the evidence artifacts: duplicates, mismatches, vendor issues, and reconciliation exceptions, each with the records behind it.

## Run it

```bash
perch ap evidence ./examples/ap-folder
```

Point it at a folder that holds the work: invoices, payment exports, vendor lists, statements, or a close package.

## Save the artifacts

```bash
perch ap evidence ./examples/ap-folder --json --out ./artifacts --timestamp run-001
```

This writes `ap_evidence.json` and related artifacts under `./artifacts`, tagged with the run id so you can compare runs over time.

## Build a review packet

```bash
perch ap packet ./examples/ap-folder
```

`ap packet` assembles a reviewable packet from the same evidence, suitable for handing to a person who has to sign off.

## Ask in plain language instead

If you would rather drive it conversationally, hand the folder to Saffron:

```bash
perch run "find duplicate payments and any vendors not in the approved master" \
  --mode agents --persona saffron --cwd ./examples/ap-folder
```

## Why this is not a chatbot answer

The duplicates and mismatches are computed from the files, not inferred by a model. Every flag comes back with the specific records side by side and the variance quantified, so a reviewer can confirm or overrule it. That is the difference between a finding you can defend and a sentence that sounds right.

See [recipe 03](03-deterministic-checks-in-ci.md) to assert exact totals from these checks in a CI pipeline.

# Sample AP folder

A small, fully synthetic accounts payable dataset for recipes [02](../../recipes/02-find-duplicate-payments.md) and [03](../../recipes/03-deterministic-checks-in-ci.md). Every vendor, invoice, and payment here is made up. The numbers are tiny on purpose so you can read the whole thing.

## Layout

This mirrors the folder shape Perch expects: supporting tables in named subfolders.

```
ap-folder/
  Purchase Orders/
    po_register.csv          approved POs by vendor
  Payments and Ledgers/
    vendor_master.csv        the approved vendor list
    march_payment_run.csv    payments that went out
```

## Planted issues

Two problems are hidden in the data on purpose, so the checks have something real to find:

1. **A duplicate payment.** `PAY-0001` and `PAY-0007` both pay invoice `INV-1001` for $11,800. The second one is recoverable exposure.
2. **An off-master vendor with no matching PO.** `PAY-0009` pays vendor `V099` (Shadow Supplies) for $5,400, but `V099` is not in `vendor_master.csv` and has no purchase order. This is the classic path for leakage and fraud.

## What Perch computes from it

Running `perch ap evidence ./examples/ap-folder --json` returns, among other metrics:

| Metric | Value |
|--------|-------|
| Total spend | $129,850 |
| Payments | 10 |
| Duplicate payment groups | 1 |
| Duplicate recoverable exposure | $11,800 |
| Payments with no matching PO | 1 |
| Missing-PO exposure | $5,400 |

These numbers are deterministic: the same folder returns the same values every run, which is why recipe 03 can assert them in CI.

> Invoice-to-PO over-approval checks use the invoice documents, which this CSV-only sample does not include, so that particular check is not exercised here. See the full datasets for that.

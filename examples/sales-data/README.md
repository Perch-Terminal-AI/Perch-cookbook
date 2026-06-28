# Sample sales dataset

A small, synthetic sales transaction dataset for recipe [05](../../recipes/05-analyze-a-spreadsheet.md). Every row is made up. The mess is intentional so the sandbox analysis has something real to find.

## Layout

```
sales-data/
  q1_sales.csv          1,430 transactions for Q1 2026
```

## Planted issues

1. **Missing customer ID.** Row TXN-1005 has an empty `customer_id`.
2. **Duplicate rows.** TXN-1001 and TXN-1004 are identical transactions.
3. **Date out of range.** TXN-1077 is dated 2026-04-01, outside Q1.
4. **Inconsistent product naming.** "Thingamajig" has no letter suffix.
5. **Bulk duplicate burst.** TXN-1372–TXN-1430 are 59 identical rows on the same date — a clear data loading error.

## What Perch computes from it

Running the recipe command returns a structured profile: schema, null rates, duplicates, outliers, and formatting inconsistencies. The numbers are deterministic because Python computes them in a sealed sandbox.

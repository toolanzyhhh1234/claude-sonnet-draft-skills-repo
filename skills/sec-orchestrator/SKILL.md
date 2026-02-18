---
name: sec-orchestrator
description: Orchestrate full SEC forensic analysis across EM1-EM7, CF1-CF3, KM1-KM2, and AA1-AA3 skills. Use when users request an end-to-end shenanigan scan and consolidated risk report.
---
# SEC Orchestrator

Run full pipeline analysis and consolidate findings.

## Workflow

1. Collect filings and period scope (recommended: latest 10-K + recent 10-Qs).
2. Run EM, CF, and KM skills; run AA skills when material M&A activity exists.
3. Aggregate and score flags by severity and cross-category consistency.
4. Perform cross-statement checks (income, cash flow, and balance-sheet alignment).
5. Produce executive summary, drill-down table, and follow-up diligence questions.

## Output

Generate a markdown report and machine-readable JSON summary with risk tiers and evidence-backed flags.

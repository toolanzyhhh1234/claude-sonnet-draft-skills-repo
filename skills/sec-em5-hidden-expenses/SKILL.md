---
name: sec-em5-hidden-expenses
description: Detect EM-5 techniques that hide expenses or losses in SEC filings. Use when reserves, assumptions, contingencies, or off-balance-sheet exposures appear aggressive.
---
# EM-5 Hidden Expenses

Identify understated expenses and concealed losses.

## Checks

- Review reserves (bad debt, warranty, loan loss, restructuring) for weakening coverage.
- Assess pension/OPEB and other assumption changes that reduce expense.
- Scan contingencies, commitments, VIE, and off-balance-sheet disclosures.
- Check for classification/presentation changes that obscure deterioration.

## Output

Return JSON with `shenanigan`, `risk_level`, `flags`, `supporting_evidence`, and `recommended_follow_up`.

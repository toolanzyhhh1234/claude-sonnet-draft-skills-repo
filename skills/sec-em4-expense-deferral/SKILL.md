---
name: sec-em4-expense-deferral
description: Detect EM-4 shifting current expenses to future periods. Use when capitalization rises, amortization slows, useful lives are extended, or impairments appear delayed.
---
# EM-4 Expense Deferral

Check for delayed expense recognition.

## Checks

- Track capitalization trends for software, marketing, and other operating-like costs.
- Review amortization/depreciation assumptions and useful-life extensions.
- Evaluate impairment timing vs business deterioration indicators.
- Compare expense ratios against peer and historical baselines.

## Output

Return JSON with `shenanigan`, `risk_level`, `flags`, `supporting_evidence`, and `recommended_follow_up`.

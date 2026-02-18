---
name: sec-aa2-acquisition-cashflow
description: Detect AA-2 acquisition-related cash flow inflation effects. Use when purchase accounting and deal structure make operating cash flow look stronger than organic economics.
---
# AA-2 Acquisition Cash Flow Inflation

Evaluate whether M&A accounting inflates CFFO optics.

## Checks

- Adjust for acquired working-capital classification effects.
- Review noncash deal financing and repayment classification.
- Compare pre/post-deal CFFO conversion with organic explanations.

## Output

Return JSON with `shenanigan`, `risk_level`, `flags`, `supporting_evidence`, `adjusted_cffo_bridge`, and `recommended_follow_up`.

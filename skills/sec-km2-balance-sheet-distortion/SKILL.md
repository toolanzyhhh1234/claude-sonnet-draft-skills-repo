---
name: sec-km2-balance-sheet-distortion
description: Detect KM-2 distortions in balance-sheet-based metrics. Use when DSO, reserve, inventory, receivable, or debt presentations may hide deterioration.
---
# KM-2 Balance Sheet Distortion

Test whether balance-sheet metrics were engineered to look healthier.

## Checks

- Recompute DSO consistently and detect method changes.
- Track reclassification of AR, notes, inventory, or debt accounts.
- Evaluate reserve coverage vs underlying credit or quality stress.
- Review off-balance-sheet debt and presentation-driven metric effects.

## Output

Return JSON with `shenanigan`, `risk_level`, `flags`, `supporting_evidence`, `adjusted_metrics`, and `recommended_follow_up`.

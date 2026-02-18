---
name: sec-km1-misleading-metrics
description: Detect KM-1 misleading non-GAAP and KPI presentation. Use when adjusted metrics, bookings, ARPU, SSS, ROIC, or EBITDA definitions/exclusions may overstate performance.
---
# KM-1 Misleading Metrics

Evaluate whether company-defined metrics fairly represent performance.

## Checks

- Audit GAAP-to-non-GAAP reconciliations for recurring exclusions.
- Test EBITDA/adjusted metrics vs cash-flow reality.
- Detect KPI definition drift across periods.
- Cross-check compensation metrics against promoted non-GAAP metrics.

## Output

Return JSON with `shenanigan`, `risk_level`, `flags`, `supporting_evidence`, `adjustments_table`, and `recommended_follow_up`.

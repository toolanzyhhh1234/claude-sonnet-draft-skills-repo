---
name: sec-em3-unsustainable-income
description: Detect EM-3 one-time or unsustainable income boosts in SEC filings. Use when earnings outperformance may rely on gains, reclassifications, reserve releases, or non-recurring items.
---
# EM-3 Unsustainable Income

Test whether earnings are inflated by temporary activities.

## Checks

- Identify gains from asset sales, settlements, or investments inside recurring performance.
- Review discontinued operations usage that offsets core weakness.
- Examine pension/investment income effects on operating optics.
- Flag reserve reversals that materially boost period earnings.

## Output

Return JSON with `shenanigan`, `risk_level`, `flags`, `supporting_evidence`, and `recommended_follow_up`.

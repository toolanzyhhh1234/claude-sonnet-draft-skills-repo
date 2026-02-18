---
name: sec-em6-income-deferral
description: Detect EM-6 shifting current income into later periods via cookie-jar behavior. Use when reserves and deferred accounts suggest earnings smoothing across periods.
---
# EM-6 Income Deferral

Detect deliberate smoothing by deferring current income.

## Checks

- Review deferred revenue and recognition-policy changes for unusual growth patterns.
- Detect oversized reserve builds in strong periods followed by future reversals.
- Flag big-bath behavior around leadership changes or strategic resets.

## Output

Return JSON with `shenanigan`, `risk_level`, `flags`, `supporting_evidence`, and `recommended_follow_up`.

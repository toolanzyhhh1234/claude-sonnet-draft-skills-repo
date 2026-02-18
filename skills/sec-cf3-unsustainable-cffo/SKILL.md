---
name: sec-cf3-unsustainable-cffo
description: Detect CF-3 temporary or unsustainable operating cash flow boosters. Use when working capital swings, accelerated collections, or one-time cash items drive CFFO.
---
# CF-3 Unsustainable CFFO

Assess quality and durability of CFFO.

## Checks

- Analyze DPO, DIO, and AR collection timing for pull-forward behavior.
- Flag one-time tax/legal/pension items materially lifting CFFO.
- Compare CFFO and net income trends over multiple quarters.

## Output

Return JSON with `shenanigan`, `risk_level`, `flags`, `supporting_evidence`, `cffo_quality_score`, and `recommended_follow_up`.

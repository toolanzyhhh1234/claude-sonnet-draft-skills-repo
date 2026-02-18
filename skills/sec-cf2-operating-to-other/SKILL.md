---
name: sec-cf2-operating-to-other
description: Detect CF-2 misclassification of operating outflows to investing/financing sections. Use when capitalization, acquisition allocation, or reclassification may overstate operating cash flow.
---
# CF-2 Operating to Other Sections

Check whether normal operating cash outflows were moved out of CFFO.

## Checks

- Review routine expense capitalization patterns.
- Evaluate acquisition-related working-capital classification.
- Inspect software development capitalization and other investing buckets.
- Flag opaque "other investing/financing" lines containing operating-like payments.

## Output

Return JSON with `shenanigan`, `risk_level`, `flags`, `supporting_evidence`, and `recommended_follow_up`.

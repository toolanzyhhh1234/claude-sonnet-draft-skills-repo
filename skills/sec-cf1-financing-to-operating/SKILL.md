---
name: sec-cf1-financing-to-operating
description: Detect CF-1 cases where financing inflows are presented as operating strength. Use when CFFO rises with receivable sales, supply-chain finance, or other financing-driven effects.
---
# CF-1 Financing to Operating

Test whether operating cash flow is inflated by financing sources.

## Checks

- Quantify AR factoring/securitization effects and adjust CFFO.
- Review supply-chain finance/reverse factoring and payable reclassification effects.
- Identify borrowings or note structures that may create operating-like optics.

## Output

Return JSON with `shenanigan`, `risk_level`, `flags`, `supporting_evidence`, `adjusted_cffo`, and `recommended_follow_up`.

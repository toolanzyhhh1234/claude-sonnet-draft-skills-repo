---
name: sec-em2-bogus-revenue
description: Detect EM-2 bogus or economically unsupported revenue in SEC disclosures. Use when related-party sales, round-trip deals, side agreements, or financing-like transactions may be recorded as revenue.
---
# EM-2 Bogus Revenue

Identify fictitious or non-substantive revenue.

## Checks

- Detect round-trip/boomerang patterns and vendor-customer overlap.
- Cross-check related-party disclosures against counterparties.
- Review reseller/intermediary revenue timing and consignment risk.
- Flag side letters, unusual return rights, and extended acceptance clauses.
- Detect financing or insurance structures potentially booked as revenue.

## Output

Return JSON with `shenanigan`, `risk_level`, `flags`, `supporting_evidence`, and `recommended_follow_up`.

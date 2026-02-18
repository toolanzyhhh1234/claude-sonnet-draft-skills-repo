---
name: sec-em1-revenue-timing
description: Detect EM-1 premature revenue recognition in SEC filings. Use when revenue accelerates unexpectedly, receivables/DSO rise, revenue policy changes, or channel stuffing is suspected.
---
# EM-1 Revenue Timing

Analyze whether revenue was recognized too early.

## Checks

- Recompute DSO with ending receivables and flag sharp QoQ/YoY jumps.
- Compare current and prior revenue-recognition footnotes for policy shifts.
- Check AR growth vs revenue growth and AR quality/reclassification changes.
- Look for bill-and-hold, consignment, sell-in vs sell-through changes, or quarter-end pushes.
- For long-term contracts, review POC estimate changes that raise revenue without matching cash.

## Output

Return JSON with `shenanigan`, `risk_level`, `flags`, `supporting_evidence`, and `recommended_follow_up`.

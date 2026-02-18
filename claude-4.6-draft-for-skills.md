Now I have comprehensive material from the book. Let me design the full skill set.

Here is a complete skill design for an AI agent performing SEC report analysis, based on the 15 shenanigans from *Financial Shenanigans (4th Ed.)*, structured for IDE-based AI agents like Claude Code or Codex CLI (which use markdown skill/tool files).

***

# SEC Forensic Analysis Agent Skills

These skills are organized into **4 modules** mirroring the book's structure. Each skill is a self-contained `.md` file suitable for Claude Code's `/skills` directory or Codex CLI's tool manifest.

***

## Skill Architecture Overview

```
skills/
├── sec_em1_revenue_timing.md
├── sec_em2_bogus_revenue.md
├── sec_em3_unsustainable_income.md
├── sec_em4_expense_deferral.md
├── sec_em5_hidden_expenses.md
├── sec_em6_income_deferral.md
├── sec_em7_expense_acceleration.md
├── sec_cf1_financing_to_operating.md
├── sec_cf2_operating_to_other.md
├── sec_cf3_unsustainable_cffo.md
├── sec_km1_misleading_metrics.md
├── sec_km2_balance_sheet_distortion.md
├── sec_aa1_acquisition_revenue.md
├── sec_aa2_acquisition_cashflow.md
├── sec_aa3_acquisition_metrics.md
└── sec_orchestrator.md
```

***

## Module 1: Earnings Manipulation (EM) Skills

### `sec_em1_revenue_timing.md` — EM Shenanigan #1: Revenue Too Soon

```markdown
# Skill: Detect Premature Revenue Recognition (EM-1)

## Purpose
Analyze SEC filings (10-K, 10-Q) for signs that revenue was recorded
before it was legitimately earned.

## Trigger
Call this skill when: revenue growth accelerates unexpectedly, DSO rises,
or revenue recognition policy footnotes change.

## Checks to Perform

### 1. Days Sales Outstanding (DSO) Analysis
- Formula: DSO = (Ending Accounts Receivable / Revenue) × 90
- Use ENDING receivables, not average, for detecting shenanigans
- Flag: DSO increase > 10 days QoQ or > 15 days YoY
- Flag: Large DSO drop following a period of rapid increase

### 2. Revenue Recognition Policy Footnote Changes
- Compare current 10-K/10-Q footnote to prior year
- Flag: Shift from "delivery" to "shipment" recognition
- Flag: Switch to Percentage-of-Completion (POC) accounting
- Flag: Change in collectability assessment policy
- Flag: New "sell-in" approach replacing prior "sell-through"

### 3. Receivables Quality Checks
- Flag: Accounts receivable growing faster than revenue
- Flag: Long-term receivables spiking (e.g., CA's 247-day DSO)
- Flag: AR converting to notes receivable (hides DSO)
- Flag: Receivables sold/securitized (lowers DSO cosmetically)

### 4. Bill-and-Hold Indicators
- Scan footnotes for "bill-and-hold" language
- Flag: Bill-and-hold initiated by the seller, not the buyer
- Flag: Revenue recognized before physical shipment

### 5. Channel Stuffing Signals
- Flag: Distributor inventory levels disclosed as elevated
- Flag: Extended payment terms offered to distributors
- Flag: Sell-in vs. sell-through policy change post-acquisition

### 6. Quarter-End Anomalies
- Flag: Quarter-end date changes
- Flag: Press releases announcing large sales right after period close
- Flag: Boomerang transactions (cash flows in both directions
  between seller and "customer")

### 7. POC Estimate Changes
- Flag: Estimate revisions on long-term contracts adding >$10M revenue
  with no corresponding cost increase
- Flag: Revenue surge without matching cash collection

## Output Format
Return a structured JSON:
{
  "shenanigan": "EM-1",
  "risk_level": "HIGH|MEDIUM|LOW",
  "flags": [...],
  "supporting_evidence": [...],  // quote exact filing text
  "recommended_follow_up": [...]
}
```

***

### `sec_em2_bogus_revenue.md` — EM Shenanigan #2: Bogus Revenue

```markdown
# Skill: Detect Fictitious/Bogus Revenue (EM-2)

## Purpose
Identify fabricated or economically vacuous revenue transactions.

## Checks to Perform

### 1. Round-Trip / Boomerang Transactions
- Scan MD&A and press releases for deals where cash flows
  simultaneously from seller to customer and back
- Flag: Vendor is also a customer in the same quarter
- Flag: Investment in a counterparty coinciding with a large sale to them

### 2. Related-Party Revenue
- Cross-check revenue counterparties against related-party footnotes
- Flag: Sales to entities with shared management, ownership, or
  recent investment relationships

### 3. Reseller / Intermediary Revenue
- Flag: Revenue recognized when shipped to a reseller not yet sold
  to end user
- Flag: Reseller commissions disproportionate to their role (>5%)
- Flag: Consignment arrangements with revenue recognized at shipment

### 4. Side Agreements and Return Rights
- Flag: Disclosures of side letters, extended return windows,
  or right-of-return clauses
- Flag: Inventory rising alongside DSO (returned goods piling up)

### 5. Financing Disguised as Revenue
- Flag: "Finite insurance" or structured financing products
  recorded as operating revenue
- Flag: Loans to customers classified as revenue

## Output Format
Same as EM-1 JSON structure.
```

***

### `sec_em3_unsustainable_income.md` — EM Shenanigan #3: One-Time Income Boosts

```markdown
# Skill: Detect One-Time or Unsustainable Income Boosts (EM-3)

## Checks to Perform

### 1. Gain Classification
- Flag: Asset sale gains included in operating income
- Flag: Investment gains or legal settlements boosting EPS
- Flag: Pension income contributing to operating results

### 2. Discontinued Operations
- Flag: Gains from discontinued ops used to offset core losses

### 3. R&D / Investment Income
- Flag: Equity method investment gains inflating net income

### 4. Reversal of Reserves
- Flag: Unusual reserve reversals boosting income
  (bad debt, warranty, restructuring)

## Output Format
Same structured JSON.
```

***

### `sec_em4_expense_deferral.md` — EM Shenanigan #4: Shift Expenses to Later Period

```markdown
# Skill: Detect Expense Deferral to Future Periods (EM-4)

## Checks to Perform

### 1. Capitalization vs. Expensing
- Flag: Sudden increase in capitalized costs (software, marketing, SG&A)
- Flag: Amortization periods extended without business justification
- Flag: Unusually low R&D expense relative to industry peers

### 2. Asset Impairment Timing
- Flag: Goodwill or intangible impairments delayed beyond obvious triggers
- Flag: Long-lived assets not written down despite declining business

### 3. Depreciation Policy Changes
- Flag: Useful life estimates extended on PP&E
- Flag: Depreciation rate declining while asset base grows

### 4. Hertz-style Multi-Category Expense Manipulation
- Flag: Non-fleet asset depreciation timing changes
- Flag: Allowances for doubtful accounts manipulated across periods

## Output Format
Structured JSON as above.
```

***

### `sec_em5_hidden_expenses.md` — EM Shenanigan #5: Hidden Expenses/Losses

```markdown
# Skill: Detect Hidden Expenses or Losses (EM-5)

## Checks to Perform

### 1. Off-Balance-Sheet Obligations
- Flag: Operating leases not yet capitalized (pre-ASC 842 filings)
- Flag: Variable interest entity (VIE) exposures understated

### 2. Reserve Manipulation
- Flag: Loan loss reserves declining while delinquencies rise
  (e.g., New Century pattern)
- Flag: Warranty reserves falling while product complexity rises
- Flag: Reserve presentation changes that obscure deterioration
  (combining reserves to hide decline in one component)

### 3. Pension/OPEB Assumptions
- Flag: Discount rate increases reducing pension expense
- Flag: Expected return on assets raised to suppress pension cost

### 4. Stock-Based Compensation
- Flag: Unexplained decline in SBC expense relative to headcount/pay

### 5. Loss-Hiding via Goodwill (Olympus-style)
- Flag: Large goodwill charges on minor acquisitions
- Flag: Acquisition prices materially exceeding fair value of assets

## Output Format
Structured JSON.
```

***

### `sec_em6_income_deferral.md` — EM Shenanigan #6: Shift Income to Later Period

```markdown
# Skill: Detect Improper Income Deferral (Cookie-Jar Reserves) (EM-6)

## Purpose
Detect management smoothing earnings by deferring current-period
income into future periods.

## Checks to Perform

### 1. Deferred Revenue Anomalies
- Flag: Deferred revenue growing faster than billings or bookings
- Flag: Deferred revenue policy changes extending recognition periods

### 2. Cookie-Jar Reserves
- Flag: Excessive restructuring charges taken during good years
- Flag: Large warranty or returns reserves established then reversed later
- Flag: Revenue withheld via overly conservative recognition policies

### 3. Big Bath Accounting
- Flag: Massive write-offs in a single quarter coinciding with
  CEO/CFO change or acquisition close
- Flag: Unusually large "one-time" charges that conveniently
  reset the baseline

## Output Format
Structured JSON.
```

***

### `sec_em7_expense_acceleration.md` — EM Shenanigan #7: Shift Future Expenses to Current Period

```markdown
# Skill: Detect Improper Acceleration of Future Expenses (EM-7)

## Purpose
Identify expenses pulled into the current period to create
a lower cost base for future reporting.

## Checks to Perform

### 1. Restructuring Charges
- Flag: Restructuring charges exceeding industry norms
- Flag: Charges taken at deal close (stub period manipulation)
- Flag: Restructuring reversals in subsequent quarters

### 2. In-Process R&D Write-offs (iPR&D)
- Flag: Large iPR&D charges at acquisition close
- Flag: iPR&D disproportionate to deal size

### 3. Inventory Write-downs
- Flag: Large inventory write-downs in acquisition stub period
- Flag: Subsequent COGS abnormally low after write-down

## Output Format
Structured JSON.
```

***

## Module 2: Cash Flow Shenanigan (CF) Skills

### `sec_cf1_financing_to_operating.md` — CF Shenanigan #1

```markdown
# Skill: Detect Financing Inflows Misclassified as Operating (CF-1)

## Checks to Perform

### 1. Accounts Receivable Securitization / Factoring
- Flag: CFFO boosted by AR sales (check investing/financing footnotes)
- Flag: Simultaneous DSO decline + CFFO surge → likely AR sale
- Formula: Adjusted CFFO = Reported CFFO - Proceeds from AR sales

### 2. Revolving Credit Facilities as Operating Inflow
- Flag: Short-term borrowings classified as operating instead of financing

### 3. Accounts Payable Financing (Vendor Financing)
- Flag: AP replaced by bank debt → repayment flows to financing, not ops
- Flag: "Supply chain financing" or "reverse factoring" programs
  (T-Mobile/Home Depot pattern)
- Flag: AP footnote longer than 2 sentences → investigate

### 4. Biovail-style Noncash Acquisition + Note Paydown
- Flag: Drug/IP rights acquired via note → note repayment classified
  as financing outflow, not operating outflow

## Output Format
Structured JSON with adjusted CFFO calculation where possible.
```

***

### `sec_cf2_operating_to_other.md` — CF Shenanigan #2

```markdown
# Skill: Detect Operating Outflows Misclassified to Other Sections (CF-2)

## Checks to Perform

### 1. CapEx vs. Operating Expense
- Flag: Routine maintenance capitalized as CapEx (WorldCom pattern)
- Flag: CapEx growing faster than revenue AND gross PP&A

### 2. Acquisition Working Capital Anomaly
- Flag: Acquired receivables/inventory classified as investing outflow
  (inflates organic CFFO)

### 3. Software Development Costs
- Flag: Capitalized software development rising as % of R&D spend

### 4. Investing Outflow Reclassification
- Flag: Operating cash payments buried in "other investing activities"

## Output Format
Structured JSON.
```

***

### `sec_cf3_unsustainable_cffo.md` — CF Shenanigan #3

```markdown
# Skill: Detect Unsustainable CFFO Boosters (CF-3)

## Checks to Perform

### 1. Working Capital Manipulation
- Compute Days Payable Outstanding (DPO):
  DPO = (Accounts Payable / COGS) × 90
- Flag: DPO surge > 10 days QoQ (vendor payment delays)
- Compute Days Inventory Outstanding (DIO):
  DIO = (Inventory / COGS) × 90
- Flag: DIO decline with no strategic explanation (buying less inventory)

### 2. Accelerated Customer Collections
- Flag: AR decline not explained by revenue decline
- Flag: Unusual discounts offered to accelerate payments (Silicon Graphics)
- Flag: Cash conversion cycle improving while business deteriorates

### 3. Tax Refunds / One-Time Cash Items
- Flag: Large tax refunds or settlements (Callaway Golf pattern)
- Flag: Pension contribution deferrals

### 4. Inventory Timing Games
- Flag: Inventory purchased at quarter start then depleted → cosmetic
  quarter-end cash balance boost (Silicon Graphics)

### 5. CFFO/Net Income Ratio
- Compute: CFFO / Net Income ratio over 8 quarters
- Flag: Ratio trending below 0.8 for 3+ consecutive quarters
- Flag: CFFO growing while net income falls (or vice versa)

## Output Format
Structured JSON with CFFO quality score.
```

***

## Module 3: Key Metric Shenanigan (KM) Skills

### `sec_km1_misleading_metrics.md` — KM Shenanigan #1

```markdown
# Skill: Detect Misleading Non-GAAP / KPI Metrics (KM-1)

## Checks to Perform

### 1. Non-GAAP Reconciliation Audit
- Pull GAAP vs. non-GAAP reconciliation tables
- Flag: Recurring items excluded from "adjusted" metrics
  (restructuring charges every quarter)
- Flag: SBC excluded from adjusted EBITDA
- Flag: Adjusted revenue > GAAP revenue (inflated billings/bookings)

### 2. EBITDA Quality Check
- Compute: EBITDA vs. CFFO gap
- Flag: EBITDA >> CFFO for 3+ consecutive quarters

### 3. Bookings / Backlog Metrics
- Flag: Bookings growing faster than revenue for 4+ quarters
  without explanation
- Flag: Definition of "bookings" changed YoY

### 4. Same-Store Sales / ARPU / ROIC
- Flag: Same-store sales metric redefined (e.g., Tween's
  "in-store inventory per sq ft" vs total)
- Flag: ARPU denominator changed (active vs. registered users)
- Flag: ROIC using invested capital definition that excludes goodwill

### 5. Compensation-Driven Metric Selection
- Cross-check executive compensation plan metrics (proxy statement)
  against reported KPIs
- Flag: Compensation tied to non-GAAP metrics that
  consistently outperform GAAP equivalents

## Output Format
Structured JSON with non-GAAP adjustments table.
```

***

### `sec_km2_balance_sheet_distortion.md` — KM Shenanigan #2

```markdown
# Skill: Detect Balance Sheet Metric Distortions (KM-2)

## Checks to Perform

### 1. DSO Calculation Changes
- Verify company's own DSO calculation method
- Flag: Switch from ending to average receivables in DSO
  (Tellabs pattern: 82 days masked as 59)
- Recompute DSO using ending balances always

### 2. Receivable Account Reclassifications
- Flag: Trade AR converted to notes receivable (Symbol Tech pattern)
- Flag: AR moved to "other assets" or long-term section
- Flag: Bank notes classified as cash (UTStarcom)

### 3. Inventory Metric Games
- Flag: New inventory sub-metric introduced when total is rising
- Flag: Inventory moved to long-term "other assets"
  (Merck's long-term inventory pattern)
- Flag: Days inventory rising 3+ consecutive quarters

### 4. Loan Loss / Reserve Presentation
- Flag: Reserve components combined to hide decline in key reserve
  (New Century pattern)
- Flag: Allowance for doubtful accounts falling despite rising DSO

### 5. Debt Metric Distortion
- Flag: Debt reclassified from current to long-term without clear reason
- Flag: Off-balance-sheet debt via operating leases, SPEs, or
  sale-leaseback transactions

## Output Format
Structured JSON with adjusted metric table.
```

***

## Module 4: Acquisition Accounting Shenanigan (AA) Skills

### `sec_aa1_acquisition_revenue.md` — AA Shenanigan #1

```markdown
# Skill: Detect Acquisition-Driven Revenue/Earnings Inflation (AA-1)

## Checks to Perform

### 1. Stub Period Manipulation
- Compare target's last pre-acquisition quarter to prior quarters
- Flag: Target revenue or earnings unusually low in stub period
- Flag: Large charges (restructuring, inventory write-down, iPR&D)
  concentrated at close

### 2. Pre-Close Revenue Inflation at Target
- Flag: Target's DSO spiking in quarters before deal close
- Flag: Unusual revenue recognition policy at target in final quarter
- Flag: Channel stuffing at target before deal closes (e.g., Salix/Valeant)

### 3. Suspicious Reserve Releases Post-Close
- Flag: Reserves established at close and released within 1-2 quarters
- Flag: Restructuring reversal > 20% of original charge

### 4. Revenue Policy Change Post-Acquisition
- Flag: Acquired unit switches revenue recognition policy
  in first quarter post-close (Medicis/Valeant sell-in pattern)
- Flag: Post-acquisition organic growth materially different
  from pre-acquisition trend

### 5. Goodwill as Loss Sink (Olympus pattern)
- Flag: Acquisition prices far exceeding book or fair value
- Flag: Goodwill on small acquisitions disproportionately large
- Flag: Write-offs via subsequent impairment of goodwill
  concentrated in previously acquired entities

## Output Format
Structured JSON with pre/post acquisition metric comparison.
```

***

### `sec_aa2_acquisition_cashflow.md` — AA Shenanigan #2

```markdown
# Skill: Detect Acquisition-Driven Cash Flow Inflation (AA-2)

## Checks to Perform

### 1. Working Capital Reclassification
- Flag: Acquired AR/inventory classified as investing outflow,
  inflating organic CFFO
- Compute: Organic CFFO = Reported CFFO - Working capital
  acquired via M&A (per purchase price allocation footnote)

### 2. Noncash Acquisition Financing (Biovail pattern)
- Flag: IP/drug rights acquired via note payable, not cash
- Flag: Note paydown classified as financing outflow → avoids
  operating cash deduction

### 3. CapEx Reclassification via Acquisition
- Flag: Organic CapEx declining post-acquisition while deal
  "investing" outflows balloon

### 4. CFFO/Net Income Cross-Check Post-Acquisition
- Compute trailing 4-quarter CFFO/NI ratio before and after deal
- Flag: CFFO improves materially post-close without organic explanation

## Output Format
Structured JSON with adjusted CFFO bridge.
```

***

### `sec_aa3_acquisition_metrics.md` — AA Shenanigan #3

```markdown
# Skill: Detect Acquisition-Driven KPI Manipulation (AA-3)

## Checks to Perform

### 1. Non-GAAP Metric Inflation via M&A
- Flag: "Adjusted" metrics strip out acquisition-related amortization
  (inflates apparent profitability of M&A-heavy model)
- Flag: Non-GAAP revenue > GAAP due to deferred revenue write-down
  at acquisition

### 2. Deferred Revenue Write-Down at Close
- Flag: Acquired deferred revenue zeroed out at acquisition
  (suppresses post-acquisition revenue, then inflates later)
- Compute: Adjusted revenue = Reported revenue + deferred revenue
  written off at acquisition close

### 3. Synergy Metrics
- Flag: Synergy targets cited without clear, auditable baseline
- Flag: "Cost synergies" not reflected in margin improvement

### 4. Same-Store / Organic Growth Metrics
- Flag: Organic growth calculated excluding acquisitions
  but acquisition-derived revenue sneaking into "organic" segment

### 5. Compensation Plan Misalignment (Valeant pattern)
- Cross-check: Are bonus metrics based on non-GAAP figures that
  benefit from acquisition accounting distortions?

## Output Format
Structured JSON with adjusted KPI table.
```

***

## Orchestrator Skill

### `sec_orchestrator.md` — Master SEC Analysis Controller

```markdown
# Skill: SEC Forensic Analysis Orchestrator

## Purpose
Run a full shenanigan scan on a company's SEC filings.
Accepts a ticker or CIK and coordinates all 15 sub-skills.

## Usage
```
/skill sec_orchestrator TICKER=AAPL FILINGS=10-K,10-Q PERIODS=8
```

## Workflow

### Step 1: Data Collection
- Fetch latest 10-K and 4 most recent 10-Qs from SEC EDGAR
  (https://data.sec.gov/submissions/CIK{cik}.json)
- Extract: Income Statement, Balance Sheet, Cash Flow Statement,
  Revenue Recognition footnote, Related Party footnote,
  Non-GAAP reconciliation tables, MD&A

### Step 2: Run All 15 Skills in Parallel Groups
**Group A (Earnings):** EM-1 through EM-7
**Group B (Cash Flow):** CF-1 through CF-3
**Group C (Key Metrics):** KM-1, KM-2
**Group D (Acquisitions, if M&A detected):** AA-1, AA-2, AA-3

### Step 3: Risk Scoring
Aggregate flags by severity:
- CRITICAL: 3+ HIGH flags from same shenanigan category
- HIGH: 2+ HIGH flags across different categories
- MEDIUM: Any MEDIUM flags
- LOW: Informational only

### Step 4: Cross-Statement Consistency Check
Apply "checks and balances" test:
- Revenue surge → verify CFFO and AR trends are consistent
- CFFO surge → verify NI and working capital are consistent
- Metric improvement → verify underlying GAAP numbers support it

### Step 5: Output Report
Generate:
1. Executive Summary (risk tier + top 5 flags)
2. Per-shenanigan drill-down table
3. Recommended follow-up data requests or questions for management
4. Comparison to prior period flags (trend analysis)

## Output Format
Markdown report + structured JSON for downstream pipeline use.

## Dependencies
All 15 sec_em/cf/km/aa skill files must be present.
Requires: SEC EDGAR API access, pandas for ratio calculations.
```

***

## Implementation Notes for Claude Code / Codex CLI

| Consideration | Recommendation |
|---|---|
| **Skill invocation** | Use `/skill sec_orchestrator` as the entry point; sub-skills called programmatically |
| **SEC data source** | SEC EDGAR Full-Text Search API + `python-sec-edgar` or `sec-api.io` |
| **Financial parsing** | Use `xbrl-parser` or `edgartools` Python library for structured XBRL extraction |
| **Ratio computation** | Inline Python via `execute_python` tool, output as CSV |
| **Footnote NLP** | Use the agent's built-in language model for footnote diff analysis (prior vs. current year) |
| **Versioning** | Store prior-period JSON outputs to enable trend flagging across filings |

The orchestrator skill ties the whole system together, running all 15 shenanigan checks and producing a consolidated risk report — covering the book's four pillars: earnings manipulation, cash flow manipulation, key metric distortion, and acquisition accounting shenanigans. [ppl-ai-file-upload.s3.amazonaws](https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/37276965/c919b76a-025e-44db-a1f2-48f4107412b7/Summary-List-of-Shenanigans.md)
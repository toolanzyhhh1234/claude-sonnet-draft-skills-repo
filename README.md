# Claude Sonnet 4.6 SEC Skill Drafts

Split skill pack for SEC forensic analysis, converted from the original single draft document into installable skill folders.

## Structure

```text
skills/
  sec-em1-revenue-timing/
  sec-em2-bogus-revenue/
  sec-em3-unsustainable-income/
  sec-em4-expense-deferral/
  sec-em5-hidden-expenses/
  sec-em6-income-deferral/
  sec-em7-expense-acceleration/
  sec-cf1-financing-to-operating/
  sec-cf2-operating-to-other/
  sec-cf3-unsustainable-cffo/
  sec-km1-misleading-metrics/
  sec-km2-balance-sheet-distortion/
  sec-aa1-acquisition-revenue/
  sec-aa2-acquisition-cashflow/
  sec-aa3-acquisition-metrics/
  sec-orchestrator/
```

Each skill folder contains a `SKILL.md` file with valid YAML frontmatter (`name` + `description`) compatible with the `skills` CLI discovery format.

## Included Source Draft

- `claude-4.6-draft-for-skills.md` (original unsplit draft)

# Vercel Skills CLI Reference

Primary source of truth:

- https://github.com/vercel-labs/skills

## High-Value Commands

- `npx skills add <source> --list`
- `npx skills add <source> --skill <name>`
- `npx skills add <source> --skill '*'`
- `npx skills add <source> --skill <name> -a codex -a claude-code`
- `npx skills add <source> --skill <name> -g`
- `npx skills list`
- `npx skills remove <name>`
- `npx skills check`
- `npx skills update`

## Notes

- Use quoted star for all skills: `--skill '*'`.
- `--list` is best as a preflight before installation.
- Prefer repository-level skill packs with `skills/<skill-name>/SKILL.md`.

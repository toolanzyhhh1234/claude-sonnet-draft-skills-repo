---
name: skills-cli-usage
description: Use the Vercel Skills CLI effectively for listing, adding, removing, and updating skills across Codex, Claude Code, and other supported agents. Trigger when users ask how to install or manage skills repositories.
---
# Skills CLI Usage

Use this skill when a task involves `npx skills` workflows.

## Quick Workflow

1. List skills in a repo:
   - `npx skills add <owner/repo-or-url-or-path> --list`
2. Install one skill:
   - `npx skills add <source> --skill <skill-name>`
3. Install all skills:
   - `npx skills add <source> --skill '*'`
4. Target specific agents:
   - `npx skills add <source> --skill <skill-name> -a codex -a claude-code`
5. Install globally:
   - `npx skills add <source> --skill <skill-name> -g`

## Management Commands

- List installed: `npx skills list`
- Find discoverable skills: `npx skills find <query>`
- Remove skills: `npx skills remove <skill-name>`
- Check updates: `npx skills check`
- Update installed skills: `npx skills update`

## Source Forms

- GitHub shorthand: `<owner>/<repo>`
- Full URL: `https://github.com/<owner>/<repo>`
- Local path: `./path-to-skills-repo`

## Reliability Rule

Use this skill for day-to-day commands. For latest CLI behavior and flags, verify against `references/vercel-skills-cli.md`.

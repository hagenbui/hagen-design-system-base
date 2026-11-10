# Hagen Design System Base skill

Agent skill for working on the Hagen Design System Base Figma file and the tier 2 app files built on it. The instructions live in `SKILL.md`.

## Install (all agents, global)

```
npx skills add hagenbui/hagen-design-system-base -g
```

This is a private repo, so the Mac running the command must be signed in to GitHub.

## Update

1. Edit `SKILL.md` here, bump its version line, add a line below, and commit.
2. Run the install command again to pull the new version into every agent.

## Versions

Minor (1.1 to 1.2): wording and process. Major (1.x to 2.0): the page format in the Figma files changes. Each app file's RULES block stamps the skill version it was last checked against.

- **1.1 (2026-11-10)**: findings from building Palm Reader.
  - Format change in the files: agent pages are spec blocks. Base: RULES, PROGRESS, LOCKS, ROADMAP, AUDIT, CHANGELOG. Tier 2: RULES, FLOWS, MAPPING, FINDINGS, CHANGELOG. Each RULES block has a "What to read, and when" table. Migrating an older app file means splitting its rules the same way and adding the "Built on" stamp.
  - New: working alongside other sessions (claims, relay and parallel modes), wrapping pitfalls, choosing a part by its job, button groups, annotation layer rules, flows page layout, the stored done check script, version stamps.
  - Proposal behind it: `proposals/2026-11-10-palm-reader-findings.md`.
- **1.0 (2026-11-06)**: first version.

## Works with

- `mobile-app-ui-design` (ceorkm/mobile-app-ui-design) for UX judgment. Its numbers never override the base rules.

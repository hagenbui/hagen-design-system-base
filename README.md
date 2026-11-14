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

- **1.4 (2026-11-14)**: screen sizes no longer written in the skill. It points to the base rule 2.1 and the `_Device` collection (the base now uses iOS 375x812 and Android 360x800). No format change in the files.
- **1.3 (2026-11-14)**: ideas from other design-system skills (Figma, Atlassian, designproject.io). New: "Describing a part" format (use for, don't use for with the alternative, pairs with, properties, states, invalid combinations, rule refs, date), two worked examples (build a screen, start a new app file), and a note to load the Figma plugin skills first. No format change in the files.
- **1.2 (2026-11-11)**: new section "Starting a tier 2 file with no rules": set up from a template (Palm Reader's block set, minus anything Palm specific), add the file's own preferences as pending lines, and turn them into rules only after the designer's OK. No format change in the files.
- **1.1 (2026-11-10)**: findings from building Palm Reader.
  - Format change in the files: agent pages are spec blocks. Base: RULES, PROGRESS, LOCKS, ROADMAP, AUDIT, CHANGELOG. Tier 2: RULES, FLOWS, MAPPING, FINDINGS, CHANGELOG. Each RULES block has a "What to read, and when" table. Migrating an older app file means splitting its rules the same way and adding the "Built on" stamp.
  - New: working alongside other sessions (claims, relay and parallel modes), wrapping pitfalls, choosing a part by its job, button groups, annotation layer rules, flows page layout, the stored done check script, version stamps.
  - Proposal behind it: `proposals/2026-11-10-palm-reader-findings.md`.
- **1.0 (2026-11-06)**: first version.

## Works with

- `mobile-app-ui-design` (ceorkm/mobile-app-ui-design) for UX judgment. Its numbers never override the base rules.

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

- **2.6 (2026-11-17)**: Button groups defer to button rules in RULES. Two or more actions on an empty state follow base rule 6.5 for width, not full width (found by a Kid Calendar rules read). No format change in the files.
- **2.5 (2026-11-17)**: SKILL.md split into a core file (about 22 KB, was 31 KB) and four reference files read only when a task needs them: references/new-app.md, wraps.md, flows.md, parallel-agents.md. Building rules point to the RULES block instead of copying its numbers. Figma plugin skills load once per session. PROGRESS and LOCKS are read in parts. The done check reports only counts that aren't zero and screenshots only touched screens. No format change in the files.
- **2.4 (2026-11-17)**: "Flows page layout" holds the full flow conventions and the Cat Translate reference (before, part of them lived only in one agent's local memory). Re-read RULES and HANDOFF after the context is summarized. Status lines no longer copy values from the files: the base rules version and the mix model status are read in the file, and a base table for choosing a part wins over the skill's list. No format change in the files.
- **2.3 (2026-11-17)**: rules carry a one-sentence "Why:" reason. Approval loop step 5: reapply each rule and propose a DONE CHECK SCRIPT check for it, and designer corrections follow the same steps. Done check runs after every batch, with three new items (fallback color matches the variable, icon stroke follows icon size, button size, radius and padding). New gotcha on bound paint fallback colors. Older rules without a reason get one the next time they are edited.
  - Full-set wraps: a wrap mirrors its base part's full variant set, styled, minus variants an app rule bans, listed under Left out on purpose. Unused base parts stay unwrapped until a screen needs one. New gotchas for extending a wrap and laying out a grown set. New done check item for variant coverage. Source: designer, from Kid Calendar rule 1.1 f.
  - No page format change, so tier 2 files only need their stamp moved to 2.3.
- **2.2 (2026-11-16)**: new section "Images and art": always make images with the OpenAI image generation connector, and ask the designer before using any other way when it can't be used. No format change in the files.
- **2.1 (2026-11-14)**: the Tier 2 Template has 15 starter wraps on App Components (46 variants), each holding a base part bound to the local App Color and text styles, listed in MAPPING with a Code column. "New app process" stage 5 starts with them. New gotcha for building wraps. No format change in the files. An app file made before this has no starter wraps: run the same wrap build in it, or duplicate the template again.
- **2.0 (2026-11-14)**: new section "New app process" (context, sitemap, visual style, wireframe, build, with the designer's OK after each stage).
  - Format change in the files: tier 2 files get two more pages, AGENT BRIEF (PROJECT) with the spec block BRIEF and AGENT SITEMAP (PROJECT) with the spec block SITEMAP, read when needed. Both are listed in the RULES "What to read, and when" table and in the PAGES line.
  - Migrating an older app file (for example Palm Reader): create both pages with the same blocks as the Tier 2 Template (`figma.spec.createOnCanvasAsync`, after `whoami` confirms specs are enabled), add the two rows to the RULES read table and the two pages to the PAGES line, then update the "Built on" stamp.
  - The Tier 2 Template (key snpHcKTKy0rzuFnC9h4570) already has both pages.
- **1.5 (2026-11-14)**: new apps start from the "Tier 2 Template" file (key snpHcKTKy0rzuFnC9h4570), duplicated by the designer, not from Palm Reader. Palm Reader's rules stay in Palm Reader. The setup steps were reworded, UX COPY is listed as a block, and two gotchas were added (font variables, tables in setContent). No format change in the files.
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

---
name: "hagen-design-system-base"
description: "Use for any work on the Hagen Design System Base Figma file or a tier 2 app file built on it: rules, tokens, components, screens, audits."
---

# Hagen Design System Base: how to work

The goal is an agent-ready mobile design system for IAA/IAP (ad and in-app-purchase monetized) apps. An agent given a prompt should be able to build a full working app from components, tokens and rules only, without inventing layout.

The rules live IN the Figma files. This skill is the process. Where this skill and the file disagree, the file wins. The designer's chat wins over both.

## Files

- Base (tier 1): "Design System Base", key MRoPpfFSMqPoSPd7LO8kOS.
  - Page AGENT RULES, text node "RULES" (40024184:3): approved rules only.
  - Page AGENT PROGRESS, text node "PROGRESS" (40024184:5): HANDOFF, findings under review, changelog.
  - Page AGENT ROADMAP, text node "ROADMAP" (40024226:541): the single work queue (F fix, A add, R agent readiness).
  - Page Design (40017001:5504): previews and test screens, placed to the right of existing frames.
- Tier 2 (one per app): a file that uses the base as a library. It has its own page AGENT RULES (PROJECT), local Typography variables, 31 local text styles with base names, a local color collection, and a page App Components. Trial file: "App Tier 2 - Test", key q8vh5DZone2kxMhE1P5zBJ (AI Palm Reader).
- QR Scan hC7jBaSrNHXQBNu0J0JrQh: old source file, read only. Never edit, sync or map it.

## Read order (every session, before any change)

1. AGENT PROGRESS: the HANDOFF block first.
2. AGENT RULES: read it in full. Do not skim.
3. AGENT ROADMAP: what to work on and in what order.
4. In a tier 2 file, also read its AGENT RULES (PROJECT) page in full.

Read each one with use_figma, e.g. `figma.root.children.find(p=>p.name==='AGENT RULES').findOne(n=>n.name==='RULES').characters`.

## Approval loop (never skip)

1. Propose with evidence: source node links, and Material 3 / Apple HIG citations where relevant.
2. If the change is visual, draw a preview on page Design (base) or on a test screen (tier 2).
3. Wait for the designer's explicit OK.
4. Then build, write the rule, and log it.

Never do these without approval:
- write or change a rule line
- add, rename or delete a token, variable, mode or text style
- change a component's structure or variants
- publish, or delete a component

Log findings that are waiting for review in AGENT PROGRESS (P = pattern, D = defect, Q = question, each with a node link and the base token it maps to). Gaps that a tier 2 app finds go in that file's findings (T items) and should get a roadmap id in the base.

## Versioning

The rules are at v0.4.x (v0.4.8 as of 2026-11-06). Never bump the version. The designer decides when. After an approved change, add a dated changelog line under the current version, newest first, on RULES and on PROGRESS.

## Core principle: plain base, tier 2 flavor

- The base stays plain and app-agnostic. Its Inter typeface and its colors are placeholders.
- Each app's look (typeface, colors, shape, effects) lives only in its tier 2 file. Never put app themes or app modes into the base.
- The designer is on Figma Pro, so extended collections are not available. Base parts cannot pick up tier 2 variables on their own, so the flavor comes from tier 2 wraps.
- Mix model (tier 2 rule 1.1, draft until the designer approves): WRAP a base instance first, and restyle it with overrides only. FORK only when the structure must change, and log the reason. Make a part LOCAL only when the base has no match, and log it as a base candidate. Name app parts <App>/<Part> and start each description with "Wraps: base X", "Fork of: base X, because ..." or "Local, no base match".
- Style each wrap once: local text styles and the app color collection. Screens use only the wraps and need no per-screen overrides. When a state changes color (like a selected tab), give the wrap its own variants.
- If a token or style is missing, it goes into the base first (with approval), gets published, and is then mirrored in tier 2.

## Building rules (summary, the RULES page is the source)

- No raw numbers. Every padding, gap, radius and stroke binds to a Dimension variable. Screen size from _Device is the only exception.
- Layout ladder 24 > 12 > 8 > 4 > 2: Content has padding 0 and gap 0. A Section has screen-padding-x 16 and section-padding-y 12. Heading to container is group-gap 12. A card has card-padding 16, gap group-gap, radius-surface, and fill bg-secondary. Rows use stack-gap 8. Text pairs use text-gap-tight / text-gap / text-gap-loose (rule 4.1).
- Screen shell: Status Bar > Header > Content > bottom bar > Nav. Zones are full width, height hugs content, and nothing is clipped. Check every screen at 402 (iOS) and at 360 (Android).
- Text uses only existing local text styles from the 7.11 pairing table. Never set fontName, fontSize or letterSpacing directly. Never create new style variants (rule 7.8).
- Use base components and the preset use cases (Dialog & Modal "Use cases", Bottom Sheet Overlay, Dialog Overlay). Never detach, and never use sub-components or modules.
- Naming: private parts start with "_". Property names are plain words with no "?". Use Material 3 / HIG terms.

## Done check (run before saying anything is done)

Run a use_figma audit on everything you touched and fix the result to zero, or report what is left:
- text nodes without a local text style, or with font, size or tracking set directly
- padding, gap, radius or stroke values that are not bound to a variable
- fills or strokes that are not bound to a color variable (system Status Bar and Nav Bar are exempt)
- detached instances, and generic layer names (Frame, Group, Vector)
- clipped frames, and screens that break the shell order
- tokens, colors or styles that don't appear in the approved lists

Then take a screenshot and look at it.

## Design judgment

Use the mobile-app-ui-design skill for UX judgment: hierarchy, thumb zone, empty, loading, error and success states, the peak-end moment, and industry conventions. Its numbers (spacing, padding, sizes, widths) never override the base rules.

For IAA/IAP apps, think about where ads and upsells fire: native ad between content blocks, banner at the bottom of content and result screens, rewarded "AD" marker inside the button, paywall, limit-reached upsell, rating prompt. The base has no ad slot, Card or Accordion parts yet (roadmap A2, A3, A11, A25). Propose them instead of improvising in the base.

## Figma gotchas

- Set `figma.skipInvisibleInstanceChildren = false` before touching hidden instance children.
- A base icon slot keeps its 20 to 32 size when swapped, so use a separate Art swap property for large art.
- The base "_Device" collection is not published because of its "_" prefix, so tier 2 files can't bind screen size (renaming it is waiting on the designer).
- Long text nodes (RULES, PROGRESS, ROADMAP) use Inter Regular: load it before editing, edit by exact string replace, and re-read afterward.

## Talking to the designer

- Plain language, no code talk, no em dashes. Short replies, and lead with the result or the ask.
- Summarize a plan before long work.
- Say clearly what changed, what didn't, and what is waiting on them.
- When you end a session, rewrite the PROGRESS HANDOFF so the next agent can start cold.
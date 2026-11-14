---
name: "hagen-design-system-base"
description: "Use for any work on the Hagen Design System Base Figma file or a tier 2 app file built on it: rules, tokens, components, screens, audits."
---

# Hagen Design System Base: how to work

**Skill version 1.3 (2026-11-14).** Changes per version: README.md.

The goal is an agent-ready mobile design system for IAA/IAP (ad and in-app-purchase monetized) apps. An agent given a prompt should be able to build a full working app from components, tokens and rules only, without inventing layout.

The rules live IN the Figma files. This skill is the process. Where this skill and the file disagree, the file wins. The designer's chat wins over both.

## Files

- Base (tier 1): "Design System Base", key MRoPpfFSMqPoSPd7LO8kOS.
  - Page AGENT RULES: spec block RULES (approved rules, read guide, rules version) and text node "DONE CHECK SCRIPT" (run it, don't read it).
  - Page AGENT PROGRESS: spec blocks PROGRESS (HANDOFF, workflow), AUDIT (QR Scan findings P/D/Q) and CHANGELOG (work log, rules versions, roadmap log).
  - Page AGENT ROADMAP: spec blocks LOCKS (who edits which base part, rule 1.1) and ROADMAP (the single work queue: F fix, A add, R agent readiness).
  - Page Design (40017001:5504): previews and test screens, placed to the right of existing frames.
  - Hidden "_OLD ... text" nodes on those pages are the pre-2026-11-10 copies. Never read or edit them.
- Tier 2 (one per app): a file that uses the base as a library. It has its own page AGENT RULES (PROJECT) with spec blocks RULES, FLOWS, MAPPING, FINDINGS and CHANGELOG, local Typography variables, 31 local text styles with base names, a local color collection, and a page App Components. Trial file: "Palm Reader", key q8vh5DZone2kxMhE1P5zBJ.
- QR Scan hC7jBaSrNHXQBNu0J0JrQh: old source file, read only. Never edit, sync or map it.

## Read order (every session, before any change)

Always read (base):
1. PROGRESS block: HANDOFF first.
2. RULES block: in full, do not skim. Its "What to read, and when" table says which other blocks a task needs.
3. LOCKS block: before editing any base part.

Read only when needed (base): ROADMAP (choosing work, updating an item), AUDIT (QR Scan audit, P/D/Q review), CHANGELOG (why or when; to log, its first 15 lines).

In a tier 2 file, also read its RULES block in full and check its "Built on" stamp (see Versioning). Open FLOWS, MAPPING, FINDINGS or CHANGELOG only when its table says the task needs them.

All agent pages are spec blocks. Find one by page and name with `page.findOne(n=>n.type==='SPEC_BLOCK'&&n.name==='RULES')`, read it with `figma.spec.getContent({specNodeId, offset, maxLines})`, and edit with `figma.spec.editContent` (exact, unique matches). Never `setContent` a block that has content unless the designer asked for a rewrite. Inside tables, write `_`, `*` and `[` plainly: escapes show up as visible backslashes there.

Rules page format (keeps every session's reading small):
- One always-read block (RULES): read guide, Claims, Changed since, settings, pattern rules, pending. Aim for 10,000 characters or less.
- Task blocks, read only when needed: FLOWS (flow layout, versions), MAPPING (part table), FINDINGS (base gaps), CHANGELOG (history).
- Use `##` sections and one `###` heading per rule, so a part of a block can be found and read alone.
- A rule is a few lines, then its source (designer, date). Point to variables instead of copying values.
- To log, read only the top of CHANGELOG and add a line under today's date.

## Working alongside other sessions

The in-file rules share knowledge, not coordination. Another agent may be editing the same file right now.
- Claim before you write. Base: a row in the LOCKS block (base rule 1.1). Tier 2: a line in the Claims section of its RULES block. Say the session, what you own (pages, flow sections, parts, blocks) and the date. Remove it when you end. Never edit what another claim holds. Write a request under it instead.
- Rules pages, PROGRESS, ROADMAP and shared parts (the app's button, header and other parts used on many screens) have one writer at a time. Claim them explicitly.
- Re-read before you write. Re-read a long text or spec right before editing it. If it changed since your first read, merge and tell the designer. Never overwrite.
- Find nodes by page and name every time. Ids from earlier in the session, from notes or from the summary can be gone.
- When you change a rule, log it so others see it: base, a line under "Rules versions" in CHANGELOG; tier 2, a line in "Changed since" on its RULES block. Before each done check, read those lines for changes by other sessions (screen sizes, renamed pages, converted nodes).
- Splitting flow sections between sessions is safe. Two sessions changing shared parts or rules is not: tell the designer and stop.

Two ways to run two agents on one file:
- **Relay (one after another, safest).** Agent A claims, works, runs the done check, rewrites HANDOFF (what changed, node names, open items, what B should do next) and releases its claim. Agent B starts with the read order, so it picks up from HANDOFF. Only one claim line exists at a time.
- **Parallel (same time).** Before either starts, the designer splits the work by area: for example A owns flow sections 1 to 6, B owns 7 to 14. Shared parts and the rules page get one owner (usually A), and the other agent writes requests under that owner's claim instead of editing. Each agent logs its changelog lines in its own block, and the owner merges them at the end. If an agent needs something outside its claim, it stops and asks, and doesn't edit.

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

Three versions, each written where an agent sees it on first read:
- **Base rules version** (v0.4.8 as of 2026-11-10): top of the base RULES block. Never bump it. The designer decides when. After an approved change, add a dated line under "Rules versions" in the base CHANGELOG, newest first.
- **Skill version** (1.1): top of this file, with changes per version in README.md. Bump it when this skill changes: minor (1.1 to 1.2) for wording and process, major (1.x to 2.0) when the page format in the files changes. Also update "Page format: skill x" on the base RULES block.
- **Tier 2 stamp**: a "Built on: base rules vX · skill Y · checked date" line under the title of each app's RULES block.

At session start in a tier 2 file, compare its stamp with the base RULES version and this skill's version:
- Base rules newer: read the base CHANGELOG "Rules versions" from the stamped version up, list the app parts it affects, tell the designer, and update the affected parts with approval. Then update the stamp.
- Skill newer: apply the format changes listed in README.md for the versions in between (for example the block split in 1.1), then update the stamp.
- Stamp missing: add it with today's versions after reading both, and say so.
- No RULES block at all: follow "Starting a tier 2 file with no rules" first.

## Starting a tier 2 file with no rules

If an app file has no page AGENT RULES (PROJECT), or that page has no RULES block, set it up before any other work. Claim the rules page first. The order is: template, then the file's own preferences on top, then the designer's OK.

1. **Template.** Copy the block set and headings from the trial file Palm Reader: RULES, FLOWS, MAPPING, FINDINGS, CHANGELOG. Keep the read guide table, Claims, Changed since, and the rules that hold for any app (mix model as a draft, choosing a part, annotation layer, no dead ends, flow layout). Leave out everything Palm specific: its typeface, colors, parts, flows and findings. Give each copied rule the source "template from Palm Reader, date".
2. **Read the file's preferences.** Without editing anything, scan what the designer already made: typefaces and sizes in use, fills, corner radius, spacing, repeated layers and their names, page and flow layout, and the app's language. Report counts with node links, not impressions.
3. **Tweak the template.** Write each preference as a pending line under the template rule it changes: "Pending: the file uses X (N nodes, link). Template says Y. Proposal: Z." A preference can change a template rule, never a base rule. Where the file breaks a base rule (raw values, detached parts), log it in FINDINGS instead.
4. **Approve.** Show the designer the pending list. Approved lines become rules with the source "designer, date". Rejected lines are removed.
5. **Finish.** Add the "Built on" stamp and a CHANGELOG line. Local Typography variables, text styles, the color collection and page App Components follow the approval loop as usual.

## Core principle: plain base, tier 2 flavor

- The base stays plain and app-agnostic. Its Inter typeface and its colors are placeholders.
- Each app's look (typeface, colors, shape, effects) lives only in its tier 2 file. Never put app themes or app modes into the base.
- The designer is on Figma Pro, so extended collections are not available. Base parts cannot pick up tier 2 variables on their own, so the flavor comes from tier 2 wraps.
- Mix model (tier 2 rule 1.1, draft until the designer approves): WRAP a base instance first, and restyle it with overrides only. FORK only when the structure must change, and log the reason. Make a part LOCAL only when the base has no match, and log it as a base candidate. Name app parts <App>/<Part> and start each description with "Wraps: base X", "Fork of: base X, because ..." or "Local, no base match".
- Style each wrap once: local text styles and the app color collection. Screens use only the wraps and need no per-screen overrides. When a state changes color (like a selected tab), give the wrap its own variants.
- If a token or style is missing, it goes into the base first (with approval), gets published, and is then mirrored in tier 2.
- Before making a new wrap, search the file for layers doing the same job or looking the same (same fill token, radius, label style), including plain base instances, and switch them in the same pass. A base part that looks identical to a wrap is drift.
- A wrap's description lists its nested base parts and says which ones can't follow the app colors yet (link the T item). Base Switch and Radio inside a wrap keep base colors.
- Before forking, write "base X can't do Y because Z" in the description and log a base candidate. If the reason is only a missing slot or property, propose that to the base first.
- At session end, mark app parts with 0 uses as "unused, delete?" in the mapping table. Don't keep them silently.

## Choosing a part (job first, look second)

Pick a part by the job it does, never by which one looks closest. If the job isn't below or in the file's rules, ask. Until the base has its own table (pending approval), use this:
- Navigate into a screen, a settings item, a saved record, a long single-choice list in a form: list row.
- Do something: button. Secondary action: ghost or secondary button, never a list row.
- Toggle: switch or checkbox. Never a row with nothing on the right.
- Status: a checklist item, not tappable.
- Two big choices: picture cards. Short picks and survey answers: option cards. Suggestions: chips.
- Share on a result: an icon button in the header.

Button groups:
- One action on an empty or error screen: Primary, hugging its label.
- Two or more actions: stacked full width, the main action first.
- Destructive is the main action: Destructive + Secondary.
- Primary plus a destructive choice plus cancel: Primary, Destructive Secondary, Ghost. One red button per group.
- A row that opens a delete confirm stays a row. The red appears on the confirm button.

## Describing a part

Every public base part and every app part has a description in this form (base roadmap F1, R1). Agents find parts through search and read this text, so write only facts the part really has.
- Use for: the job it does.
- Do not use for: each wrong job, with the part to use instead.
- Pairs with: the parts it sits with or inside, and where (bottom bar, header, List Card).
- Properties: only those that exist, with defaults. No hypothetical variants.
- States: the ones the part has.
- Invalid combinations: what must not be set together, written as the problem plus the fix.
- Rule refs and the date last reviewed.

App parts also start with "Wraps: ...", "Fork of: ..." or "Local, no base match" (mix model). Set a description only on a component or component set, never on an instance.

## Building rules (summary, the RULES page is the source)

- No raw numbers. Every padding, gap, radius and stroke binds to a Dimension variable. Screen size from _Device is the only exception.
- Layout ladder 24 > 12 > 8 > 4 > 2: Content has padding 0 and gap 0. A Section has screen-padding-x 16 and section-padding-y 12. Heading to container is group-gap 12. A card has card-padding 16, gap group-gap, radius-surface, and fill bg-secondary. Rows use stack-gap 8. Text pairs use text-gap-tight / text-gap / text-gap-loose (rule 4.1).
- Screen shell: Status Bar > Header > Content > bottom bar > Nav. Zones are full width, height hugs content, and nothing is clipped. Check every screen at 402 (iOS) and at 360 (Android).
- Text uses only existing local text styles from the 7.11 pairing table. Never set fontName, fontSize or letterSpacing directly. Never create new style variants (rule 7.8).
- Use base components and the preset use cases (Dialog & Modal "Use cases", Bottom Sheet Overlay, Dialog Overlay). Never detach, and never use sub-components or modules.
- Naming: private parts start with "_". Property names are plain words with no "?". Use Material 3 / HIG terms.
- The annotation layer follows the same rules: jump tags, case labels, notes and preview boards. Build each one once as a part with styles and tokens, and instance it. Never build tags or labels from raw text in a script.
- After a new pattern or part, scan the whole file for the same job (text, layer names, part usage) and reapply it in the same pass. Log what you replaced and what you left on purpose, with the reason.
- No dead ends: every button, icon and link on a flows page ends in an arrow or a jump tag to the screen it opens.

## Flows page layout

- One section per feature, stacked in one left-aligned column. The happy path runs left to right in one row.
- Cases (errors, empty states, alternative results) go in darker sub-sections under the step they branch from, with their screens stacked vertically.
- Only straight arrows (the API can't set bend points). Use horizontal arrows between neighbors and vertical drops into the case below. Every other link becomes a pair of jump tags ("→ 2.1c · Skip" / "← 1.6 · Skip"). Arrows never overlap screens or other arrows.
- Hubs (Home, Settings, lists): put each destination on its own row below the hub, with spine arrows from the hub's bottom edge. Never chain them as if each went deeper.
- Name screens "number Flow => State". Notes sit next to the screen they explain.
- Later releases go on their own page and hold only the sections that change. Shared parts get a switch that is off by default.

## Done check (run before saying anything is done)

Run the base text node "DONE CHECK SCRIPT" (page AGENT RULES, base rule 10.1) exactly as written: read it from the base file, set ROOT_ID and APP_PREFIX ('Palm/' style in an app file), run it in the file you're checking, and report its counts. It covers most items below. Check the rest by hand, never a subset, and name any item you skipped. Never say "clean" or "uses the file's styles" without counts behind it. Annotation layers count.
- text nodes without a local text style, with font, size or tracking set directly, with a style from another library, or with a style not in the 7.11 table
- padding, gap, radius or stroke values that are not bound to a variable
- fills or strokes that are not bound to a color variable (system Status Bar and Nav Bar are exempt)
- detached instances, and generic layer names (Frame, Group, Vector)
- clipped frames, and screens that break the shell order
- tokens, colors or styles that don't appear in the approved lists
- instances whose fills, strokes or effects differ from their main component (leftover overrides)
- screen sizes against the current rule (re-read it, another session may have changed it)

Then take a screenshot and look at it. Rewrite the HANDOFF block if it's older than the newest changelog line.

## Examples

**Build a screen.** Prompt: "Add a Result screen with a share action and two follow-up actions."
- Read order, then claim the flow section you own.
- Search the file for a screen doing the same job and reuse its pattern (reapply rule).
- Build only from the app's wraps and base parts, bound to tokens. Share is a header icon button. The two follow-ups are stacked full width, Primary first, then Ghost (Choosing a part, Button groups).
- Every action ends in an arrow or jump tag. Notes are in Vietnamese.
- Run the done check, paste its counts, take a screenshot, log a CHANGELOG line, release the claim.

**Start a new app file.** Prompt: "Start a new app called X on the base."
- Read the base RULES and check the base version and this skill's version.
- The file has no RULES block, so follow "Starting a tier 2 file with no rules": template, scan the file, pending lines, designer's OK, stamp.
- Ask the designer for what the base can't decide: screen size, typeface, colors, and whether IAA is on. Never invent them.
- Add the app's rules page, local Typography, text styles and color collection only through the approval loop.

## Design judgment

Use the mobile-app-ui-design skill for UX judgment: hierarchy, thumb zone, empty, loading, error and success states, the peak-end moment, and industry conventions. Its numbers (spacing, padding, sizes, widths) never override the base rules.

For IAA/IAP apps, think about where ads and upsells fire: native ad between content blocks, banner at the bottom of content and result screens, rewarded "AD" marker inside the button, paywall, limit-reached upsell, rating prompt. The base has no ad slot, Card or Accordion parts yet (roadmap A2, A3, A11, A25). Propose them instead of improvising in the base.

## Figma gotchas

- This skill sits on top of the Figma plugin skills and does not repeat their API rules. Before any `use_figma` call, load `figma-use`. Also load `figma-generate-design` when you draw or change a screen, and `figma-generate-library` when you build a part, a variable collection or a style. Pass the names in `skillNames`.
- A component description stores a straight apostrophe as `&#39;` and a straight double quote as `&quot;`. Write "Do not" instead of "Don't", and use curly quotes or none. Read a description back after writing it.
- `figma.getNodeByIdAsync(id)` reaches nodes on other pages without switching the current page, so one call can read or set many parts.
- Set `figma.skipInvisibleInstanceChildren = false` before touching hidden instance children.
- A base icon slot keeps its 20 to 32 size when swapped, so use a separate Art swap property for large art.
- The base "_Device" collection is not published because of its "_" prefix, so tier 2 files can't bind screen size (renaming it is waiting on the designer).
- The DONE CHECK SCRIPT is still a text node in Inter Regular: load the font before editing it, edit by exact string replace, and re-read afterward.
- When swapping an instance to another variant or part, call `resetOverrides()` first, then set only what you need. Old fills and hidden icons survive a swap otherwise.
- Never make a tint with paint or layer opacity on a variable-bound paint: it doesn't reach instances. Bind a real token or ask for one.
- A screen with FILL content inside a hugging root collapses. Give the screen root the device minHeight and let Content hug.
- Not available in this context: `figma.loadAllPagesAsync`, `figma.createConnector`, connector bend points. `findAll` doesn't exist on text nodes: check `'findAll' in node` first.
- Keep reads of big files small (compact JSON, small screenshots). Large responses break.

## Talking to the designer

- Plain language, no code talk, no em dashes. Short replies, and lead with the result or the ask.
- In app files, every annotation, sticky note and dev note is in Vietnamese. Screen copy stays in the app's language, and image prompts stay in English.
- Summarize a plan before long work.
- Say clearly what changed, what didn't, and what is waiting on them.
- When you end a session, rewrite the PROGRESS HANDOFF so the next agent can start cold.
---
name: "hagen-design-system-base"
description: "Use for any work on the Hagen Design System Base Figma file or a tier 2 app file built on it: rules, tokens, components, screens, audits."
---

# Hagen Design System Base: how to work

**Skill version 2.8 (2026-11-18).** Changes per version: README.md.

The goal is an agent-ready mobile design system for IAA/IAP (ad and in-app-purchase monetized) apps. An agent given a prompt should be able to build a full working app from components, tokens and rules only, without inventing layout.

The rules live IN the Figma files. This skill is the process. Where this skill and the file disagree, the file wins. The designer's chat wins over both.

## Files

- Base (tier 1): "Design System Base", key MRoPpfFSMqPoSPd7LO8kOS.
  - Page AGENT RULES: spec block RULES (approved rules, read guide, rules version) and text node "DONE CHECK SCRIPT" (run it, don't read it).
  - Page AGENT PROGRESS: spec blocks PROGRESS (HANDOFF, workflow), AUDIT (QR Scan findings P/D/Q) and CHANGELOG (work log, rules versions, roadmap log).
  - Page AGENT ROADMAP: spec blocks LOCKS (who edits which base part, rule 1.1) and ROADMAP (the single work queue: F fix, A add, R agent readiness).
  - Page Design (40017001:5504): previews and test screens, placed to the right of existing frames.
  - Hidden "_OLD ... text" nodes on those pages are the pre-2026-11-10 copies. Never read or edit them.
- Tier 2 (one per app): a file that uses the base as a library. It has its own page AGENT RULES (PROJECT) with spec blocks RULES, FLOWS, MAPPING, FINDINGS, SKILL FINDINGS, CHANGELOG and UX COPY, a page AGENT BRIEF (PROJECT) with the block BRIEF, a page AGENT SITEMAP (PROJECT) with the block SITEMAP, local Typography variables, 31 local text styles with base names, a local color collection, and a page App Components.
  - New apps start from "Tier 2 Template", key snpHcKTKy0rzuFnC9h4570: a clean file with those pages, blocks and styles and neutral placeholder values. The designer duplicates it (file name menu > Duplicate) and sends the link of the copy. A file can't be duplicated from the API, and enabling the base library in a new file is also the designer's step.
  - The template's page App Components has 15 starter wraps: App/Button, Header, ListItem, ListCard, InputField, BottomNavigation, BottomNavTab, DialogOverlay, BottomSheetOverlay, Badge, Switch, CheckBox, Radio, EmptyState and PageIndicator. Each holds a base part bound to the local App Color and text styles, so an app restyles them by changing variables. Rename App to the app's short name. They are listed in MAPPING. Limits: Switch, Check Box and Radio keep their inner base colors (finding T2), and the dim of the overlays keeps the base scrim color. Starter wraps follow the full-set rule (Core principle): when an app starts, check each one against its base part and add the missing variants.
  - Trial file: "Palm Reader", key q8vh5DZone2kxMhE1P5zBJ. Its rules are Palm's own and stay there. Never copy rules from it into another file.
- QR Scan hC7jBaSrNHXQBNu0J0JrQh: old source file, read only. Never edit, sync or map it.

## Read order (every session, before any change)

Always read (base):
1. PROGRESS block: the HANDOFF section only (read with offset and maxLines, not the whole block).
2. RULES block: in full, do not skim. Its "What to read, and when" table says which other blocks a task needs.
3. LOCKS block: before editing any base part. Find the rows you need, not the whole table.

Read again when your context was summarized or cut: before the next write, re-read RULES in full and HANDOFF, and re-find nodes by page and name. A summary is not the rules.

Read only when needed (base): ROADMAP (choosing work, updating an item), AUDIT (QR Scan audit, P/D/Q review), CHANGELOG (why or when; to log, its first 15 lines).

In a tier 2 file, also read its RULES block in full and check its "Built on" stamp (see Versioning). Open FLOWS, MAPPING, FINDINGS, SKILL FINDINGS or CHANGELOG only when its table says the task needs them. BRIEF and SITEMAP are separate pages, read when needed: BRIEF when you start the app, choose a feature or are asked why a screen exists, SITEMAP when you add, remove or link screens.

All agent pages are spec blocks. Find one by page and name with `page.findOne(n=>n.type==='SPEC_BLOCK'&&n.name==='RULES')`, read it with `figma.spec.getContent({specNodeId, offset, maxLines})`, and edit with `figma.spec.editContent` (exact, unique matches). Never `setContent` a block that has content unless the designer asked for a rewrite. Inside tables, write `_`, `*` and `[` plainly: escapes show up as visible backslashes there.

Rules page format (keeps every session's reading small):
- One always-read block (RULES): read guide, Claims, Changed since, settings, pattern rules, pending. Aim for 10,000 characters or less.
- Task blocks, read only when needed: FLOWS (flow layout, versions), MAPPING (part table), FINDINGS (base gaps), SKILL FINDINGS (lessons about how agents work), CHANGELOG (history).
- Use `##` sections and one `###` heading per rule, so a part of a block can be found and read alone.
- A rule is a few lines, then "Why:" with the reason in one sentence, then its source (designer, date). The reason is what an agent works from when it hits a case the rule doesn't cover, so never drop it. If the designer gave no reason, ask. Point to variables instead of copying values.
- To log, read only the top of CHANGELOG and add a line under today's date.

## Reference files (read only when the task needs them)

These sit next to this file. They hold steps you need for some tasks only, so a session reads less.

| File | Read when |
|---|---|
| references/new-app.md | starting a new app, a tier 2 file with no rules, or any stage of the new app process |
| references/wraps.md | building, extending, forking or describing a part, or changing a font variable |
| references/flows.md | drawing, moving or linking screens on a flows page |
| references/parallel-agents.md | the designer wants two agents on one file |
| references/skill-findings.md | writing, merging or reviewing a skill finding |

If you can't open a reference file, say so and ask. Never guess its steps.

## Working alongside other sessions

The in-file rules share knowledge, not coordination. Another agent may be editing the same file right now.
- Claim before you write. Base: a row in the LOCKS block (base rule 1.1). Tier 2: a line in the Claims section of its RULES block. Say the session, what you own (pages, flow sections, parts, blocks) and the date. Remove it when you end. Never edit what another claim holds. Write a request under it instead.
- Rules pages, PROGRESS, ROADMAP and shared parts (the app's button, header and other parts used on many screens) have one writer at a time. Claim them explicitly.
- Re-read before you write. Re-read a long text or spec right before editing it. If it changed since your first read, merge and tell the designer. Never overwrite.
- Find nodes by page and name every time. Ids from earlier in the session, from notes or from the summary can be gone.
- When you change a rule, log it so others see it: base, a line under "Rules versions" in CHANGELOG; tier 2, a line in "Changed since" on its RULES block. Before each done check, read those lines for changes by other sessions (screen sizes, renamed pages, converted nodes).
- Splitting flow sections between sessions is safe. Two sessions changing shared parts or rules is not: tell the designer and stop.

To run two agents on one file (relay or parallel), read references/parallel-agents.md.

## Approval loop (never skip)

1. Propose with evidence: source node links, and Material 3 / Apple HIG citations where relevant.
2. If the change is visual, draw a preview on page Design (base) or on a test screen (tier 2).
3. Wait for the designer's explicit OK.
4. Then build, write the rule with its reason, and log it.
5. Make it stick. Apply the rule to every screen and part already drawn (reapply scan). If a script can check the rule, propose adding that check to the DONE CHECK SCRIPT in the same pass, so the next session catches it without being told. The script is a base node, so this follows this loop too.

A designer correction goes through the same steps: fix the screen, then the rule and reason, the check and the reapply. The designer should never have to say the same thing twice.

Never do these without approval:
- write or change a rule line
- add, rename or delete a token, variable, mode or text style
- change a component's structure or variants
- publish, or delete a component

Log findings that are waiting for review in AGENT PROGRESS (P = pattern, D = defect, Q = question, each with a node link and the base token it maps to). Gaps that a tier 2 app finds go in that file's findings (T items) and should get a roadmap id in the base.

## Skill findings (lessons inbox)

Each tier 2 file has a block SKILL FINDINGS on AGENT RULES (PROJECT): evidence about how agents work, kept for the designer to review. FINDINGS stays for base part gaps.
- Collect a finding when the designer corrects you, you repeat a mistake, an instruction misled you or was missing, a tool behaved in a way this skill doesn't warn about, a check was missing, or a base/app mismatch teaches a workflow lesson. One app's visual preference is an app rule, not a finding.
- Write only during write work you are authorized for, into an existing block. If the cause matches an open item, add an "Also seen" line to it instead of a new id.
- No block in the file: propose the finding in chat. Creating the block or editing RULES is rules maintenance and needs its own OK. An OK to build a screen is not one.
- Read-only task: propose findings in chat and write nothing to Figma. In base work, propose lessons in chat too.
- A designer correction still becomes an app rule through the Approval loop. The finding records only the workflow lesson.
- Findings are evidence, not rules. Never change this skill from them. Only the designer moves an item to Reviewed, Approved or Rejected (an agent may reject a duplicate as merged).
- At session end, list the open SF ids (Status not Applied or Rejected) in your report. When you are authorized to write and the block exists, also update its Handoff section.
- Format, statuses, merging and the review steps: references/skill-findings.md.

## Versioning

Three versions, each written where an agent sees it on first read:
- **Base rules version**: top of the base RULES block. Read it there, never from notes or this skill. Never bump it. The designer decides when. After an approved change, add a dated line under "Rules versions" in the base CHANGELOG, newest first.
- **Skill version**: top of this file, with changes per version in README.md. Bump it when this skill changes: minor (1.1 to 1.2) for wording and process, major (1.x to 2.0) when the page format in the files changes. Also update "Page format: skill x" on the base RULES block.
- **Tier 2 stamp**: a "Built on: base rules vX · skill Y · checked date" line under the title of each app's RULES block.

At session start in a tier 2 file, compare its stamp with the base RULES version and this skill's version:
- Base rules newer: read the base CHANGELOG "Rules versions" from the stamped version up, list the app parts it affects, tell the designer, and update the affected parts with approval. Then update the stamp.
- Skill newer: apply the format changes listed in README.md for the versions in between (for example the block split in 1.1), then update the stamp. A format change that creates a block or edits RULES needs the designer's rules maintenance OK first. Without it, leave the stamp and say which changes are pending.
- Stamp missing: add it with today's versions after reading both, and say so.
- No RULES block at all: follow "Starting a tier 2 file with no rules" in references/new-app.md first.

## Core principle: plain base, tier 2 flavor

- The base stays plain and app-agnostic. Its Inter typeface and its colors are placeholders.
- Each app's look (typeface, colors, shape, effects) lives only in its tier 2 file. Never put app themes or app modes into the base.
- The designer is on Figma Pro, so extended collections are not available. Base parts cannot pick up tier 2 variables on their own, so the flavor comes from tier 2 wraps.
- Mix model (tier 2 rule 1.1; its status is per app, so read rule 1.1 in the file's RULES block, and if it is still a draft there, follow it and say so): WRAP a base instance first, and restyle it with overrides only. FORK only when the structure must change, and log the reason. Make a part LOCAL only when the base has no match, and log it as a base candidate. Name app parts <App>/<Part> and start each description with "Wraps: base X", "Fork of: base X, because ..." or "Local, no base match".
- Style each wrap once: local text styles and the app color collection. Screens use only the wraps and need no per-screen overrides. When a state changes color (like a selected tab), give the wrap its own variants.
- FULL SET: a wrap mirrors every variant of its base part (every Style or Emphasis, Size, State and option such as Icon, Selected, Delete, Label, Scrollable), each one styled, so the designer can switch to any option inside the app look. Never wrap only the variants the current screens use. The only gaps are variants an app rule bans (for example Shadow On when the app has no shadows, Hover on touch apps); the description ends with "Left out on purpose: ... (reason)" or "Left out on purpose: none." A wrap may draw a state itself (Pressed by a lip) instead of using the base state; say so in the description. Destructive base parts become extra styles of the same wrap (Destructive, Destructive Secondary, Destructive Ghost; Danger on icon buttons).
- Base parts the app does not use are not wrapped ahead of time: an unstyled App/ part looks app-ready to agents and is drift. Wrap a part the first time a screen needs it, as a full set, styled in the same pass.
- If a token or style is missing, it goes into the base first (with approval), gets published, and is then mirrored in tier 2.
- Before making a new wrap, search the file for layers doing the same job or looking the same (same fill token, radius, label style), including plain base instances, and switch them in the same pass. A base part that looks identical to a wrap is drift.
- A wrap's description lists its nested base parts and says which ones can't follow the app colors yet (link the T item). Base Switch and Radio inside a wrap keep base colors.
- Before forking, write "base X can't do Y because Z" in the description and log a base candidate. If the reason is only a missing slot or property, propose that to the base first.
- At session end, mark app parts with 0 uses as "unused, delete?" in the mapping table. Don't keep them silently.

## Choosing a part (job first, look second)

Pick a part by the job it does, never by which one looks closest. If the job isn't below or in the file's rules, ask. If the base RULES block has a table for choosing a part, it wins over this list. Otherwise use this:
- Navigate into a screen, a settings item, a saved record, a long single-choice list in a form: list row.
- Do something: button. Secondary action: ghost or secondary button, never a list row.
- Toggle: switch or checkbox. Never a row with nothing on the right.
- Status: a checklist item, not tappable.
- Two big choices: picture cards. Short picks and survey answers: option cards. Suggestions: chips.
- Share on a result: an icon button in the header.

Button groups (a button rule in the base or app RULES block wins over this list):
- One action on an empty or error screen: Primary, hugging its label.
- Two or more actions: stacked, the main action first. Full width on most screens. On empty states, follow the base empty state rule (6.5) for their width.
- Destructive is the main action: Destructive + Secondary.
- Primary plus a destructive choice plus cancel: Primary, Destructive Secondary, Ghost. One red button per group.
- A row that opens a delete confirm stays a row. The red appears on the confirm button.

## Describing a part

Every public base part and every app part has a description in a fixed form (Use for, Do not use for, Pairs with, Properties, States, Invalid combinations, rule refs). Before you write or change one, read references/wraps.md.

## Building rules (the RULES page is the source)

You read the RULES block in full, so its numbers are not copied here (layout ladder, screen shell, text styles, components). The ones most often broken: no raw numbers, text only from local text styles (7.11, 7.8). Also:
- Use base components and the preset use cases (Dialog & Modal "Use cases", Bottom Sheet Overlay, Dialog Overlay). Never detach, and never use sub-components or modules.
- Naming: private parts start with "_". Property names are plain words with no "?". Use Material 3 / HIG terms.
- The annotation layer follows the same rules: jump tags, case labels, notes and preview boards. Build each one once as a part with styles and tokens, and instance it. Never build tags or labels from raw text in a script.
- After a new pattern or part, scan the whole file for the same job (text, layer names, part usage) and reapply it in the same pass. Log what you replaced and what you left on purpose, with the reason.
- No dead ends: every button, icon and link on a flows page ends in an arrow or a jump tag to the screen it opens.

## Flows page layout

Read references/flows.md before you draw, move or link screens on a flows page.

## Done check (run after every batch, and before saying anything is done)

A batch is one flow section, one set of parts or one rule reapply. Run the check over the whole file after each batch, not only once at the end, so mistakes don't spread into the next batch.

Run the base text node "DONE CHECK SCRIPT" (page AGENT RULES, base rule 10.1) exactly as written: read it from the base file, set ROOT_ID and APP_PREFIX ('Palm/' style in an app file), run it in the file you're checking, and report its counts. It covers most items below. Check the rest by hand, never a subset, and name any item you skipped. Never say "clean" or "uses the file's styles" without counts behind it. Annotation layers count.
- text nodes without a local text style, with font, size or tracking set directly, with a style from another library, or with a style not in the 7.11 table
- padding, gap, radius or stroke values that are not bound to a variable
- fills or strokes that are not bound to a color variable (system Status Bar and Nav Bar are exempt)
- bound fills or strokes whose stored fallback color differs from the variable's resolved value (see Figma gotchas)
- icon vectors whose stroke weight doesn't follow the icon size rule in RULES (if RULES has none, log a Q finding)
- buttons whose height, radius or padding don't match their size variant
- detached instances, and generic layer names (Frame, Group, Vector)
- clipped frames, and screens that break the shell order
- tokens, colors or styles that don't appear in the approved lists
- instances whose fills, strokes or effects differ from their main component (leftover overrides)
- screen sizes against the current rule (re-read it, another session may have changed it)
- every wrap you touched covers its base part's full variant set, except what its description lists under "Left out on purpose" (compare the base set's variant properties with the wrap's)

Report the check compactly: only counts that aren't zero, with up to 10 node ids each, never full node dumps. Then take a screenshot of the screens you touched, at a small size, and look at it. A screenshot shows resolved variables, so it can't show wrong bindings or fallback colors: the counts come first, the screenshot second. Rewrite the HANDOFF block if it's older than the newest changelog line.

## Example

**Build a screen.** Prompt: "Add a Result screen with a share action and two follow-up actions."
- Read order, then claim the flow section you own.
- Search the file for a screen doing the same job and reuse its pattern (reapply rule).
- Build only from the app's wraps and base parts, bound to tokens. Share is a header icon button. The two follow-ups are stacked full width, Primary first, then Ghost (Choosing a part, Button groups).
- Every action ends in an arrow or jump tag. Notes are in Vietnamese.
- Run the done check, paste its counts, take a screenshot, log a CHANGELOG line, release the claim.

## Design judgment

Use the mobile-app-ui-design skill for UX judgment: hierarchy, thumb zone, empty, loading, error and success states, the peak-end moment, and industry conventions. Its numbers (spacing, padding, sizes, widths) never override the base rules.

For IAA/IAP apps, think about where ads and upsells fire: native ad between content blocks, banner at the bottom of content and result screens, rewarded "AD" marker inside the button, paywall, limit-reached upsell, rating prompt. The base has no ad slot, Card or Accordion parts yet (roadmap A2, A3, A11, A25). Propose them instead of improvising in the base.

## Images and art

- Always make images (illustrations, icons as art, photos, backgrounds, style tile art) with the OpenAI image generation connector. Write the prompt in English.
- If that connector isn't available in this session, fails, or can't make what's needed (size, transparency, format), stop and ask the designer first. Say why it can't be used and which other way you would use (for example Figma's generate_image, a vector illustration, or a placeholder). Never switch to another image tool on your own.
- Until art is approved, use the Illustration text box (references/new-app.md, stage 4).

## Figma gotchas

- This skill sits on top of the Figma plugin skills and does not repeat their API rules. Load `figma-use` once per session, before the first `use_figma` call. Load `figma-generate-design` once when you first draw or change a screen, and `figma-generate-library` only when you build a part, a variable collection or a style. Don't load them again in the same session.
- Gotchas for building and extending parts are in references/wraps.md, and adding a spec block is in references/new-app.md.
- `figma.getNodeByIdAsync(id)` reaches nodes on other pages without switching the current page, so one call can read or set many parts.
- `figma.spec.setContent` on a block that has a table can fail with "ambiguous table column correspondence". Write the block with a placeholder line, then put the table in with `editContent`.
- Set `figma.skipInvisibleInstanceChildren = false` before touching hidden instance children.
- The base screen size collection is "Device" (renamed from "_Device" on 2026-11-17) and is published, so tier 2 screens can bind screen-width and screen-height to it. Older notes that say "_Device" mean the same collection.
- The DONE CHECK SCRIPT is still a text node in Inter Regular: load the font before editing it, edit by exact string replace, and re-read afterward.
- When swapping an instance to another variant or part, call `resetOverrides()` first, then set only what you need. Old fills and hidden icons survive a swap otherwise.
- A paint bound to a color variable still stores a raw color, the fallback. Never write black or a placeholder there. Set it to the variable's value for that node: `const { r, g, b } = variable.resolveForConsumer(node).value`, then bind. A wrong fallback looks right in screenshots and only shows when the file is opened or the binding breaks.
- Never make a tint with paint or layer opacity on a variable-bound paint: it doesn't reach instances. Bind a real token or ask for one.
- A screen with FILL content inside a hugging root collapses. Give the screen root the device minHeight and let Content hug.
- Not available in this context: `figma.loadAllPagesAsync`, `figma.createConnector`, connector bend points. `findAll` doesn't exist on text nodes: check `'findAll' in node` first.
- Keep reads of big files small (compact JSON, small screenshots). Large responses break.

## Talking to the designer

- Plain language, no code talk, no em dashes. Short replies, and lead with the result or the ask.
- In app files, every annotation, sticky note and dev note is in Vietnamese. Screen copy stays in the app's language, and image prompts stay in English.
- Summarize a plan before long work.
- Say clearly what changed, what didn't, and what is waiting on them.
- When you end a session in the base, rewrite the PROGRESS HANDOFF so the next agent can start cold. In a tier 2 file, report the open SF ids (see Skill findings).
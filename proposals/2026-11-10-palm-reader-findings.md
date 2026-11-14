# Palm Reader findings: proposed skill improvements

Source: the two Palm Reader sessions on 2026-11-09 and 2026-11-10 (designer messages, agent reports, 316 use_figma calls, 25 failed calls). Status 2026-11-14: items 1 to 5 landed in skill 1.1 (wrapping gotchas, annotation layer rule, stored done check, choosing a part, claims). Skill 1.2 added the no-rules setup and 1.3 the part description format. The base RULES text for choosing a part and button groups still waits for the designer's approval. Each item says what happened, why, and the proposed change to SKILL.md (and where a rule belongs in Figma instead).

## 1. Drift when wrapping components

**What happened**
- Swapped instances kept old overrides (white fill, icons). 7.4a stayed solid red after the style changed. 4.4a and 7.4a needed fills copied from the main part by hand.
- Destructive Secondary used paint opacity on a bound color. The opacity did not reach instances, so copies rendered solid red. It was rebuilt twice (16% tint, then Ghost fill plus rose border).
- Dialog Cancel buttons look like Palm/Button Ghost but are still the plain base Button. Two parts, one look.
- Nested base parts inside a wrap (Switch, Radio) keep base colors, because base colors can't be themed per app (T2). The wrap only restyles its own top layer.
- Palm/HomeHeader was forked because the base Header has no slot for a chevron. Forks like this were decided per screen, not checked against the mix model.
- Unused parts piled up (ChatBubble, ProfileChip, HandOption, BottomNav) with no cleanup step.

**Why:** the skill says "WRAP, restyle with overrides only" but not how overrides behave on swap, which properties survive to instances, or what to do about nested base parts.

**Proposed SKILL.md change (new "Wrapping gotchas" under Figma gotchas)**
- After swapping an instance to another variant or part, call `resetOverrides()` first, then set only the properties you need. Then compare fills, strokes and effects to the main component; any difference is a leftover override.
- Never use paint opacity or layer opacity on a variable-bound paint to make a tint. Bind to a real token (or ask for one).
- Before making a new wrap, search the file for layers that already look like it (same fill token, same radius, same label style) and switch them to the wrap in the same pass. Base parts that look identical to a wrap are drift.
- A wrap must list its nested base parts in its description and say which ones can't follow the app colors yet (link the T item).
- Fork check: before forking, write one line "base X can't do Y because Z" and add it as a base candidate. If the reason is only a missing slot or property, propose the slot to the base first.
- End of session: list app parts with 0 uses in the mapping table as "unused, delete?" instead of keeping them silently.

## 2. Missing text styles (and raw values) on helper layers

**What happened**
- The jump tag helper (about 74 tags plus the flow arrows) set `fontName` Manrope SemiBold and `fontSize` 14 directly, with raw padding 12/6, radius 16 and a raw purple fill. It ran 7 times.
- The done check reported clean anyway. On 2026-11-10 the check that ran was a reduced one: colors, spill and empty text only, no text style check.
- Credit packs (Color Dream): discount badges had no text style, four layers used styles from another library, and the big "20" used a style the file doesn't have. A previous session had claimed it used the file's styles.

**Why:** the skill's rules only talk about screens and parts. Annotation layers (jump tags, stickies, case labels, preview boards) have no rule, so agents treat them as exempt and write raw values. And the done check is described as a list, not as one script, so each session runs its own partial version.

**Proposed change**
- Add an "Annotation layer" rule: tags, labels and notes use a small set of parts (Flow/JumpTag, Flow/CaseLabel, Flow/Note) built once with styles and tokens. Never build them from raw text in a script. (The parts themselves go in the tier 2 file with approval.)
- Make the done check one fixed script stored in the file (for example a text node "DONE CHECK" on AGENT RULES), and have the skill say: run that script as written, paste its counts, never a hand-picked subset. If a check is skipped, say which one.
- Add to the check: text whose style comes from another library, and text styles not in the 7.11 table.
- Never claim "uses the file's styles" without the script's count behind it.

## 3. Missing context on when and how to use parts (buttons, button groups, list rows)

**What happened**
- Secondary CTAs on error screens were built as list rows with chevrons, under a small pill primary. The designer asked "why secondary CTA is a list row?"
- A scan found 129 list rows on 42 screens. About half were misused: actions, toggles with no control, status, two-option picks, profile picks, chat suggestions, survey picks. After the fix, 83 remain.
- Button Style variants were added one at a time as the designer asked (Destructive, then Destructive Secondary, then Ghost) with no pairing table, so the agent didn't know Primary + Destructive + Ghost needs a secondary destructive.
- Single actions vs stacks: an empty state button went full width and had to be reverted to hug (rule 6.5 / 2.14).
- The 2.11 to 2.18 project rules now cover this, but only in Palm Reader. The base has no "use when / don't use when" for its own parts.

**Why:** the skill and base rules say which parts exist and how to bind tokens, but not which part does which job. Agents pick the part that "looks closest" and List Item is the most flexible base part, so it gets overused.

**Proposed change**
- Base, new rule section "Choosing a part" (job to part table), seeded from Palm Reader 2.12 to 2.15:
  - Navigate into a screen, settings, saved records, long single-choice list in a form: List Item.
  - Do something: Button. Secondary action: Ghost/Secondary button, never a row.
  - Toggle: Switch or Checkbox, never a bare row.
  - Status: checklist item, not tappable.
  - 2 big choices: picture cards. Short picks: option cards or chips.
  - Suggestions: chips.
- Base, new "Button groups" rule: allowed combinations and order, for example
  - one action on empty or error screen: Primary, hugs its label
  - Primary + Secondary: stacked full width, Primary first
  - Destructive main action: Destructive + Secondary
  - Primary + Destructive + Cancel: Primary, Destructive Secondary, Ghost; one red button per group
  - Bottom bar vs in-content placement
- Every base component description gets "Use for / Don't use for / Pairs with" (this extends roadmap F1/R1, which already asks for descriptions).
- SKILL.md: before placing any part, look up its job in "Choosing a part". If the job isn't in the table, ask instead of picking the closest-looking part.

## 4. Process gaps

- **Reapply new patterns** and **no dead ends** were taught by correction (rule 2.11, 2.17). Move both into the skill's building steps for every tier 2 file, not only Palm Reader: after a new part, scan and reapply; every action ends in an arrow or jump tag.
- **Flow layout** (rule 2.16, Cat Translate conventions) lives only in Palm Reader and in local memory. Move it into the skill (or a base rule) so other agents and machines get it.
- **Vietnamese notes** is in memory only. Put it in the skill's "Talking to the designer" section for app files.
- **API limits learned the hard way:** `loadAllPagesAsync` and `createConnector` aren't available in this context, connector waypoints can't be set, `findAll` doesn't exist on text nodes, and large reads from big files break the response. Add to Figma gotchas.
- **Screen collapse:** FILL content inside a hug screen collapsed screens. Add: screen root keeps minHeight of the device and Content hugs.
- **Stale HANDOFF:** the handoff was 3 days older than the changelog. Make "rewrite HANDOFF" part of the done check, not only "when you end a session".

## 5. Two agents on the same file at the same time

Short answer: no. The in-file rules are enough to share knowledge, not to coordinate. During Palm Reader, a second session at the same time:
- converted the rules text node into a spec block (old node id gone, scripts failed with null),
- renamed FLOWS to Design,
- rebuilt 1.5 and replaced its art, turned Palm/Aura into a set,
- changed rule 2.3 screen size from 402 to 375×812, so this session ran its width checks against the old size without knowing.

About 12 of the 25 failed calls were null nodes or missing ids caused by this. Nothing was lost, but only because the agent re-read and re-found nodes by name.

**What's missing, and the proposed fix**
- **Claims.** Add a CLAIMS block at the top of AGENT PROGRESS: one line per active session, with session name, what it owns (pages, flow sections, parts), and start time. Read it first; claim before writing; release at the end. Never edit what another session has claimed; log a request under it instead.
- **One writer for shared pages.** Rules, PROGRESS and App Components are edited by one session at a time (claim them). Others append requests, not edits.
- **Re-read before write.** Before editing a long text or spec, re-read it and compare with what you read earlier. If it changed, merge and report, never overwrite. (The Palm session did this once by luck; make it a rule.)
- **Find by name, not by saved id.** Ids from earlier in the session or from notes can be gone. Look nodes up by page and name each time.
- **Rule changes announce themselves.** A rule change by one session adds a line to a "Changed since" list on PROGRESS. Other active sessions check it before each done check.
- **Different parts, not different screens.** Two sessions can safely split flow sections. They can't safely both change shared parts (Palm/Button, HomeHeader) or the rules; that work should be one session.

## Suggested order

1. Done check as one stored script (fixes item 2, cheap, prevents false "clean").
2. Claims block and re-read-before-write (item 5).
3. Wrapping gotchas in SKILL.md (item 1).
4. "Choosing a part" and "Button groups" rules in the base, with your approval and a preview (item 3).
5. Move flow layout, reapply, no dead ends and Vietnamese notes into the skill (item 4).

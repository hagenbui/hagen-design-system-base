# Skill findings: format and review

Part of the hagen-design-system-base skill. Read when you write, merge or review a skill finding. The boundaries in SKILL.md ("Skill findings") always apply: write only during authorized write work, never change the skill from a finding, and only the designer reviews or approves.

## The block

Block SKILL FINDINGS on page AGENT RULES (PROJECT) of each tier 2 file. Find it with `page.findOne(n=>n.type==='SPEC_BLOCK'&&n.name==='SKILL FINDINGS')`. Its shape:

```
# SKILL FINDINGS (PROJECT): <App name>

<intro line>

## SF-1 · <short title>
- Seen: ...
...

## Handoff

<open SF ids and what each waits on>
```

Field labels stay in English so every agent finds them. The text after a label follows the file's note language (Vietnamese in app files). Keep existing text when you restructure an item: move it into the fields, don't translate or shorten it.

## Entry format

```
## SF-<n> · <short title>
- Seen: <date> · <app> · session <id> · skill <x.y>
- Kind: correction | repeated mistake | instruction gap | tool pitfall | missing check | base/app mismatch
- Evidence: <Figma links> · observed: <what happened> · expected: <what should have> · rule: <ref, or none>
- Cause: Confirmed: <what you checked> / Hypothesis: <not yet checked>
- Rule existed: ignored <rule ref> | unclear <where> | none
- Lesson: <one sentence, the smallest reusable change>. Why: <one sentence>
- Status: Collected | Reviewed | Approved (<who>, <date>) | Applied | Rejected (<reason>)
- Tracks: App fix <none | open | done, evidence> · Base <none | open, roadmap id | done> · Skill <none | proposed | applied>
- Applied: skill <x.y> · <file and section> · verified by <evidence> · limits <what is not covered>
- Also seen: <date> · session <id> · <one line>
```

Leave out "Applied" until Status is Applied, and "Also seen" until it happens.

## Field rules

- Ids never get reused. Rejected items stay, with the reason.
- Status is about the lesson only. An agent writes Collected. The designer moves an item to Reviewed (seen it), Approved (promote it into the shared skill) or Rejected, and only in so many words: "looks fine" is not an approval, so ask. The one agent move is "Rejected (merged into SF-n)". Applied means the skill version with the lesson is committed and its README line is written.
- Open means Status is not Applied or Rejected.
- App fixes and base changes live in Tracks and never move Status. An approved design intent (for example "equal button heights") goes in the Base or App track, not as Status Approved.
- Cause: "Confirmed" only for what you checked in the file or in tool output. Everything else is "Hypothesis".
- Rule existed: "ignored" means the instruction was there and the agent didn't follow it. The fix is then a check, not a new rule.
- Lesson: the smallest change that would have prevented it, in this order of preference: a check in the DONE CHECK SCRIPT, a clearer instruction, a gotcha. A new rule comes last.
- One app's look (a lip, a color, a radius) is not a lesson. It belongs in that app's RULES.

## Merging duplicates

- Same root cause as an open item: add an "Also seen" line there. A different symptom of the same cause is still the same item.
- Two items turn out to share a cause: keep the older id, move the newer one's evidence into it, and mark the newer one "Rejected (merged into SF-n)".
- Before adding an item, read the block's headings (the `##` lines) and the Cause lines of open items.

## Review and promotion (the designer starts it)

1. The designer asks for a review. Read the SKILL FINDINGS block of each app file the request names. Never say an app was checked without reading its block.
2. Group items by cause across apps. Show each group in chat: the lesson, how many times it was seen and where, and the smallest change.
3. Wait for an explicit approval per item. Then change the skill, bump its version, add the README line (name the SF ids and apps it came from), and update "Page format: skill x" on the base RULES block.
4. In each app file where you have the rules maintenance OK, set Status Applied and fill in the Applied line. Without that OK, list in chat the ids still to update.

## Adding the block to a file that has none

Only with the designer's rules maintenance OK, and with a line in the file's RULES Claims.
1. `whoami`, check `specs_enabled`. On page AGENT RULES (PROJECT), `figma.spec.createOnCanvasAsync({ title: 'SKILL FINDINGS', content })`, placed clear of the other blocks. Read it back by name.
2. Content: the title line, the intro line below, an empty items part and a `## Handoff` section with "Không có mục mở."
3. Intro line: "Bằng chứng để cải thiện skill, không phải quy tắc. FINDINGS giữ thiếu sót của base. Trạng thái: Collected → Reviewed → Approved → Applied, hoặc Rejected. Chỉ designer duyệt. Định dạng: references/skill-findings.md trong skill."
4. Add this row to the RULES "What to read, and when" table, after the FINDINGS row: `| SKILL FINDINGS | Logging a designer correction, a repeated mistake or a tool pitfall; reviewing skill lessons; ending a write session with open items | Read-only work, or no lesson and no open item |`
5. Move the "Built on" stamp and add a "Changed since" line.

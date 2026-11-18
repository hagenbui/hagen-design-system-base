# Skill findings inbox: proposal

Date: 2026-11-18. Status: applied in skill 2.8 on 2026-11-18 (designer approved; numbered 2.8, not 3.0, at the designer's request). Migrated: base page format line and CHANGELOG, Tier 2 Template, Kid Calendar. Palm Reader pending. Open questions settled: English field labels with text in the file's note language; base sessions propose lessons in chat. The text below is the original proposal; the skill and references/skill-findings.md are the source.

Original status: proposal, nothing applied. Skill stays 2.7, no Figma file changed. Read for this: SKILL.md 2.7, README, and in Kid Calendar (e32WhXyTyBhDKJhW06YQwW) the draft block SKILL FINDINGS (node 4248:6592), the RULES read guide and the FINDINGS header (read only).

## What is there now

- Kid Calendar has a block SKILL FINDINGS on AGENT RULES (PROJECT) with SF-1 to SF-3, a status line and a handoff, written in Vietnamese. Its RULES read guide already has a SKILL FINDINGS row.
- The draft is reusable as is. Three things need fixing when it is migrated:
  1. SF-3 says "Trạng thái: Approved". What you approved is the design intent (equal heights, square icon buttons). The lesson ("trace to the base first, compare button families of the same size") is not approved. Under this proposal SF-3 is Status Reviewed, with Base track "intent approved, not built, not published", App track "open", Skill track "proposed".
  2. A RULES "Changed since" line (2026-11-18) still says "Skill 3.0". The next line says the skill was reverted to 2.7. The 3.0 line should be corrected so no agent reads it as a released version.
  3. Fields are written as one long paragraph per item. A fixed field list (below) is easier for an agent to update, dedupe and review.
- Side note: Kid Calendar's RULES block is 16,332 characters, above the 10,000 target. Not part of this change.

## 1. Skill wording (core SKILL.md, about 10 lines)

New section, placed after "Approval loop":

```
## Skill findings (lessons inbox)

Each tier 2 file has a block SKILL FINDINGS on AGENT RULES (PROJECT): evidence about how agents work, kept for the designer to review. FINDINGS stays for base part gaps.
- Collect a finding when the designer corrects you, you repeat a mistake, an instruction misled you or was missing, a tool behaved in a way the skill doesn't warn about, a check was missing, or a base/app mismatch teaches a workflow lesson.
- Write only during write work you are authorized for, into an existing block. If the cause matches an open item, add an "Also seen" line to it instead of a new id.
- No block in the file: propose the finding in chat. Creating the block or editing RULES is rules maintenance and needs its own OK; an OK to build a screen is not one.
- Read-only task: propose findings in chat, write nothing to Figma.
- Findings are evidence, not rules. Never change this skill from them. The designer approves each promotion.
- List open SF ids in your handoff.
- Format, statuses and the review steps: references/skill-findings.md.
```

Plus one row in the core "Reference files" table:

```
| references/skill-findings.md | writing, merging or reviewing a skill finding |
```

## 2. Where the detail lives

New file references/skill-findings.md (about 3 KB). The core keeps only when to collect and the boundaries above, so every session pays for 10 lines, not the format.

Proposed content:

### Entry format

```
## SF-<n> · <short title>
- Seen: <date> · <app> · session <id> · skill <x.y>
- Kind: correction | repeated mistake | instruction gap | tool pitfall | missing check | base/app mismatch
- Evidence: <Figma links> · observed: <what happened> · expected: <what should have> · rule: <ref, or none>
- Cause: Confirmed: <what was checked> / Hypothesis: <not yet checked>
- Rule existed: ignored <rule ref> | unclear <where> | none
- Lesson: <one sentence, the smallest reusable change>. Why: <one sentence>
- Status: Collected | Reviewed | Approved (<who>, <date>) | Applied | Rejected (<reason>)
- Tracks: App fix <none | open | done, evidence> · Base <none | open, roadmap id | done> · Skill <none | proposed | applied>
- Applied: skill <x.y> · <file and section> · verified by <evidence> · limits <what is not covered>
- Also seen: <date> · session <id> · <one line>
```

Rules for the fields:
- Ids never get reused. Rejected items stay, with the reason.
- Status is about the lesson only. Approved means the designer approved promoting the lesson into the shared skill. Applied means a released skill version contains it.
- An app fix or a base change never moves Status. They live in Tracks. Approval of design intent is written in Tracks (Base or App), not as Status Approved.
- Cause: write "Confirmed" only for what you checked in the file or the tool output. Everything else is "Hypothesis".
- "Rule existed: ignored" means the instruction was there and the agent didn't follow it. The fix is then a check, not a new rule.
- The "Applied" line is filled only when Status is Applied.
- Field labels stay in English so agents can find them. The text after a label follows the file's note language (Vietnamese in app files).

### Deduplication

- Same root cause as an open item: add an "Also seen" line there. A different symptom of the same cause is still the same item.
- Two items turn out to share a cause: keep the older id, move the other's evidence into it, mark the newer one "Rejected (merged into SF-n)".

### Promoting a lesson (designer-led review)

1. The designer asks for a review. Read the SKILL FINDINGS block of each app file named in the request. Never claim an app was checked without reading its block.
2. Group items by cause across apps. Show each group in chat: the lesson, the evidence count, and the smallest change. In order of preference, the smallest change is a new check in the DONE CHECK SCRIPT, then a clearer instruction, then a gotcha. A new rule comes last.
3. Leave out one app's visual preference (for example Kid Calendar's 4 px lip). It belongs in that app's RULES.
4. Wait for an explicit approval per item. Then change the skill, bump its version, and write the README line.
5. With rules maintenance OK in each app file, set Status Applied and fill in the Applied line. Without that OK, list the ids to update in chat.

## 3. Migration steps (not done yet)

The tier 2 page format changes (a new block), so this is skill 3.0 under the README versioning rule.

1. Skill: add the core section and the reference row, add references/skill-findings.md, bump to 3.0, and add a README line with these migration steps. Also update "Page format: skill" on the base RULES block.
2. Tier 2 Template (snpHcKTKy0rzuFnC9h4570): add an empty SKILL FINDINGS block (title, one intro line pointing to the skill reference, no items) on AGENT RULES (PROJECT), and a read guide row in its RULES. Check that the block reads back, then set the template stamp to 3.0.
3. Kid Calendar: keep block 4248:6592. Rewrite SF-1 to SF-3 into the field format without losing content, and fix SF-3's status as described above. Fix the "Skill 3.0" Changed since line. Move the stamp to 3.0 and add a Changed since line.
4. Palm Reader (q8vh5DZone2kxMhE1P5zBJ): read its rules page first. Add the block and the read guide row only if it has none. Move the stamp.
5. Any other app file: check it at its next session through the stamp (skill newer → apply format changes). Don't claim it was migrated before checking.

Each file needs the designer's rules maintenance OK and a claim in its RULES Claims section.

Not in this change: the SF-3 base work (Button and IconButton equal heights). It belongs to a base-owning session through the approval loop and a roadmap id.

## 4. Behavioral tests

Run each in a fresh session, ideally on two models (Claude and the OpenCode model), on a duplicate of Kid Calendar or on the template. Pass means the observed file state matches. The agent's own report doesn't count.

| # | Setup and prompt | Pass when |
|---|---|---|
| 1 Collect | Authorized screen build. The designer says "gap should be 8, not 12". | The screen is fixed. A new SF item has Kind correction and Status Collected. SKILL.md is unchanged (git diff empty). |
| 2 Dedupe | Authorized wrap work that hits a remote Inter style inside a slot. | SF-1 gains an "Also seen" line. No new SF id. |
| 3 Read-only | "Review the Palm Reader home screen." | Findings appear in chat. The file's version history shows no edit from the session. |
| 4 Missing inbox | A file with no SKILL FINDINGS block, and an OK to build one screen. | No block is created and RULES is not edited. The finding is proposed in chat with a request for rules maintenance OK. |
| 5 Approval | The designer says "SF-2 looks fine". | Nothing changes in the skill or Status. The agent asks whether this approves promotion. After an explicit "approve SF-2", the skill changes, the version is bumped, and SF-2 is Applied with its version, location and verification. |
| 6 Tracks | The app fix for SF-1 is done and the skill is unchanged. | Status is not Applied. Tracks shows App fix done and Skill proposed. |
| 7 Preference | The designer asks to promote the 4 px lip. | The agent says it is one app's look, keeps it in Kid Calendar RULES, and proposes no shared rule. |
| 8 Handoff | A session ends with open items. | The handoff lists their SF ids. |

## Open questions for the designer

1. Language: field labels in English and text in Vietnamese (as proposed), or the whole block in Vietnamese like the current draft?
2. Should base sessions also collect skill findings? If so, where: a block on the base AGENT PROGRESS page, or the existing AUDIT block?

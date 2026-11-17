# Empty state rules: proposed base rule

Source: Palm Reader, frame "Content" (node 68:8753, file q8vh5DZone2kxMhE1P5zBJ), slot 5.3a "Free questions used up". Read on 2026-11-16 through the Figma MCP. This is the working example named by the designer. The rules below are taken from what it does. Status: draft, all open questions decided 2026-11-16, written to the base on 2026-11-16 by extending rule 6.5 EMPTY STATE (not a new section, because 6.5 already existed; designer approved). Logged in the base CHANGELOG, version not bumped.

## The example

A 402 x 718 content area, one centered column, no header text, no extra chrome:

| # | Section | Contents | Notes |
|---|---------|----------|-------|
| 1 | Art | `Palm/Art/State/QuestionsUsedUp`, 120 x 120 | Local art, transparent PNG, one image per state. |
| 2 | Text | Title + body, centered | Title: Title/title-md-semibold (Cormorant Garamond 28/36). Body: Text/text-md-regular (Manrope 16/24), `fg-secondary`. |
| 3 | Action | One `Palm/Button` (Primary, lg), label "Back to chat" | Hugs its content (142 x 56), centered. Never full width. |

Layout: vertical auto layout, centered on both axes, gap 0 between sections. Each section is its own frame with screen-padding-x (16) and section-padding-y (12). Spacing between art, text and button comes from the section padding plus the in-section gap, not from spacers.

Copy: the title says the state in plain words ("You used today's 3 free questions"). The body says what happens next and what still works ("You'll get 3 new questions at midnight. You can still read this chat and your past answers.").

## Proposed rules

1. **Structure.** An empty state is three sections in this order: art, text, action. Skip the art or the action only when the state has none (see 6 and 7). Never add a fourth block.
2. **Position.** Centered on both axes in the content area, left to the layout to do (no fixed y offsets).
3. **Art.** One 120 x 120 local art part (always 120, approved by the designer) per state, named `Palm/Art/State/<StateName>`. Do not reuse one image for two states. Art follows the local art rule (2.7).
4. **Text.** One title (Title/title-md-semibold, `fg-primary`) and one body (Text/text-md-regular, `fg-secondary`), both centered, both fill the section width. The title names the state. The body says what happens next and what the user can still do. Two to three lines at most.
5. **Gap.** Title to body uses text-gap-loose (8). Section to section uses the section padding (12 each side, art to text 12 + 12). Use bound tokens, never raw numbers.
6. **Action.** One to three `Palm/Button`, size lg, stacked vertically and centered, never list rows. Allowed sets, top to bottom: Primary; Primary + Ghost; Primary + Secondary; Primary + Secondary + Ghost; Primary + Ghost + Ghost. Primary is always first and there is only one. A single button hugs its content (6.5 / 2.14). Two or three buttons share one width: the stack hugs its widest button, and the other buttons fill that width. The stack is centered, never full screen width (approved by the designer 2026-11-16). In Figma: stack frame hugs, widest button hugs, the others are set to fill container. Labels are verbs that leave the state ("Back to chat"). If the state resolves itself (waiting for a timer, loading new content), omit the buttons.
7. **Errors and no-result states** use the same layout. Swap the art, the copy and the button label ("Try again", "Clear filters"). Do not invent a second layout for them.
8. **Flow placement.** Empty states are cases, so they sit in a darker sub-section under the step they branch from (SKILL.md, Flow layout). Name the screen "number Flow => Empty: <state>".

## Open questions for the designer

- Decided 2026-11-16: art is 120 x 120 for every empty state. Up to 3 buttons (Primary/Secondary/Ghost or Primary/Ghost/Ghost).
- Decided 2026-11-16: a single button hugs. With 2 or 3 buttons the stack hugs the widest one and the rest fill to match it.
- Decided 2026-11-16: the rules go in a new base section "Empty states", separate from "Choosing a part". Section number is picked when writing to the base file.

## If approved

- Base RULES text: add the eight rules above under the new "Empty states" section.
- SKILL.md: one line in the flow layout section pointing at the rule, and one in the done check ("empty state follows base rule N").
- Optional: a base `EmptyState` part (art slot, title, body, button slot) so agents stop rebuilding it per screen.

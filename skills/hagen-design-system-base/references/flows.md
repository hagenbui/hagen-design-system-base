# Flows page layout

Part of the hagen-design-system-base skill. Read when you draw, move or link screens on a flows page. SKILL.md still applies.

Reference file: Cat Translate, key sTy5BEZfV9mWWZeKBHRdQF, page "Update 29/10/2025" (node 11892-137229). Read it when a layout case isn't covered below. If the file's FLOWS block says otherwise, the block wins.

- One section per feature, short name, stacked in one left-aligned column, all the same width. Sections are dark so screens stand out (the reference uses #444444; in our files use the annotation parts and tokens, and propose one if it's missing).
- The happy path runs left to right in one row. A feature with several modes or entries has a vertical spine from the entry screen down the left side, with one row per mode.
- Cases (errors, empty states, alternative results, variants like Dog vs Cat) go in darker sub-sections named by the case, right after or under the step they branch from, with their screens stacked vertically so each case stays one column under its step.
- Small state variants (keyboard open, typing) sit directly under their base screen, in the same column.
- Arrows are one accent color with a short label naming the trigger or condition ("Record", "Pass", "Close"). Only straight arrows (the API can't set bend points): horizontal between neighbors at the same y, and vertical drops from a step's bottom center into the case below. Every other link becomes a pair of jump tags in the same color ("→ 2.1c · Skip" / "← 1.6 · Skip"). Arrows never overlap screens or other arrows.
- Hubs (Home, Settings, lists): hub top left, each destination on its own row below, with spine arrows from the hub's bottom edge turning right into each row. Spread the start points (rightmost for the top row) so spines never touch. Never chain them as if each went deeper.
- Name screens "number Flow => State". Notes are stickies next to the screen or case they explain, in Vietnamese, never one big note per section.
- Optional action callout: a small frame showing the tapped element, placed by the arrow it triggers.
- Later releases go on their own page and hold only the sections that change. Shared parts get a switch that is off by default.

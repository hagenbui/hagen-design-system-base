# Wraps and part descriptions

Part of the hagen-design-system-base skill. Read when you build, extend, fork or describe a part (a wrap, a base part or a local part), or change a font variable. The rules for when to wrap (Core principle) stay in SKILL.md.

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

## Gotchas for parts

- Building a wrap: import the base part by key (`importComponentSetByKeyAsync`), put an instance inside a new component, set `isExposedInstance = true` on it so its properties stay editable, then rebind its fills and strokes from base Semantic variables to local App Color variables, and its text to the local text style of the same name. Restyling can make some nested node ids disappear ("node does not exist"): wrap each node in try and catch, and run a second pass on overlays. A base part with no properties (for example Floating Close Button) can't be exposed: wrap isExposedInstance in try and catch and say so in MAPPING.
- Extending a wrap to its full set: list the base set's variants, then for each missing one clone the closest styled wrap variant (same style and state), call swapComponent on its "Base (styling only)" instance to the target base variant, put back the fills and strokes saved before the swap, copy the padding and itemSpacing bindings from the new base main component (old size overrides survive a swap), and set text to the local style for the new size. Then sweep the whole set: every remote color variable to its App Color slot, every remote text style to the local one of the same name, and report what is left. Icons in a new size lose their color override because the icon node changes. A wrap that gains a property (Size, Label, Icon) needs every existing variant renamed to include it first; screen instances keep working.
- After a set grows: lay its variants out in a grid (rows by style, columns by size and state), resize the set, widen its section, shift the nodes to its right, and check top-level overlaps. A screenshot taken inside the same script can show variable colors as black; check with get_screenshot before fixing anything.
- A component description stores a straight apostrophe as `&#39;` and a straight double quote as `&quot;`. Write "Do not" instead of "Don't", and use curly quotes or none. Read a description back after writing it.
- A base icon slot keeps its 20 to 32 size when swapped, so use a separate Art swap property for large art.
- Changing a FONT_FAMILY or weight variable can fail with "unloaded font Noto Sans ..." because the text styles briefly fall back. Load the named Noto fonts and the new fonts first, then set the values. Inter's semibold style is "Semi Bold" with a space.

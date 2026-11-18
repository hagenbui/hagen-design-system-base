# New app: setup and process

Part of the hagen-design-system-base skill. Read when you start a new app, set up a tier 2 file that has no rules, or work through a stage of the new app process. SKILL.md still applies.

## Starting a tier 2 file with no rules

If an app file has no page AGENT RULES (PROJECT), or that page has no RULES block, set it up before any other work. Claim the rules page first. The order is: template, then the file's own preferences on top, then the designer's OK.

1. **Template.** A new app is a duplicate of the Tier 2 Template (see Files). It already has the blocks RULES, FLOWS, MAPPING, FINDINGS, SKILL FINDINGS, CHANGELOG and UX COPY as skeletons, with the read guide table, Claims, Changed since, the mix model draft and empty Settings. Replace "App name" and set the stamp. If an older app file has no rules page, copy the block set and headings from the Tier 2 Template, never from Palm Reader. Palm's rules (its typeface, colors, parts, flows, findings, Premium tone) stay in Palm Reader. Give each rule you take from the template the source "template, date".
2. **Read the file's preferences.** Without editing anything, scan what the designer already made: typefaces and sizes in use, fills, corner radius, spacing, repeated layers and their names, page and flow layout, and the app's language. Report counts with node links, not impressions.
3. **Tweak the template.** Write each preference as a pending line under the template rule it changes: "Pending: the file uses X (N nodes, link). Template says Y. Proposal: Z." A preference can change a template rule, never a base rule. Where the file breaks a base rule (raw values, detached parts), log it in FINDINGS instead.
4. **Approve.** Show the designer the pending list. Approved lines become rules with the source "designer, date". Rejected lines are removed.
5. **Finish.** Add the "Built on" stamp and a CHANGELOG line. Local Typography variables, text styles, the color collection and page App Components follow the approval loop as usual.

## New app process

Five stages, in this order. Each one ends with the designer's OK, and the next one does not start before it. Record each stage in the file. If a stage needs facts you don't have, ask. Never invent the PO's knowledge.

1. **Context.** Read what the designer and the PO give you (documents, links, Figma, Drive). Write the page AGENT BRIEF: goal, audience, platforms and languages, features, monetization, references, constraints, open questions. Mark every unknown "to confirm". Gate: the brief is confirmed.
2. **Sitemap.** Write the tree on the page AGENT SITEMAP: feature, then screen, then state, numbered the way FLOWS will be. A visual tree below it or in FigJam is optional, and the outline stays the source. Gate: the sitemap is approved.
3. **Visual style.** Draft the typeface, look and style (RULES 2.1, 2.2, 2.4) and fill the App Color and Typography values. Show one style tile on page Design: a sample screen next to the tokens. Gate: the style is approved, and only then written as rules.
4. **Wireframe.** Draw the sitemap screens in grayscale from base parts only, with the Illustration text box for art and Ad Slot for ads. The base is already plain, so it is the wireframe kit. Then write the parts needed list in MAPPING: base part used, missing (a FINDINGS T item), or custom (wrap, fork, local). Gate: the parts list is approved.
5. **Build.** Start with the template's starter wraps (rename App to the app name; they follow the App Color and Typography values from stage 3), then base instances, then other custom parts per the mix model (wrap first), then polish: done check, reapply scan, states, copy, art, both screen sizes. Gate: each screen and each custom part.

Do not draw screens for stage 4 or 5 before stage 3 is approved. The Tier 2 Template already has the BRIEF and SITEMAP pages, so stages 1 and 2 start by filling them.

## Example

**Start a new app file.** Prompt: "Start a new app called X on the base."
- Read the base RULES and check the base version and this skill's version.
- Ask the designer to duplicate the Tier 2 Template and send the link. Then follow "Starting a tier 2 file with no rules": template, scan the file, pending lines, designer's OK, stamp.
- Ask the designer for what the base can't decide: screen size, typeface, colors, and whether IAA is on. Never invent them.
- Add the app's rules page, local Typography, text styles and color collection only through the approval loop.

## Gotcha

- To add a spec block (a new BRIEF or SITEMAP page), call `whoami` first and check `specs_enabled`, create the page, switch to it, then `figma.spec.createOnCanvasAsync({ title, content })`. Give it a non-empty title: the title becomes the block name you find it by.

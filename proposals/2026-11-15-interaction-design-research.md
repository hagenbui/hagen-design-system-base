# Interaction design research: what to add to the base

Date: 2026-11-15. Status: proposal, nothing approved, no rule or token changed.

## 1. What the system covers today (based on SKILL.md 2.1 only; not yet checked against the base RULES and ROADMAP blocks in Figma, which win over the skill)

- Structure is strong: tokens, layout ladder, shell order, wraps, done check.
- Interaction is thin. Only these exist: "Choosing a part" (job first), "Button groups", "No dead ends" on flows, a loose "states" in the polish step, and a description field "States: the ones the part has".
- Missing entirely: a state model, touch target sizes, feedback timing, motion tokens, screen transitions, loading and error patterns, gesture rules, haptics, reduced motion, and the interaction rules for ads and purchases (the app type this system is for).

### Checked against the base file (2026-11-15, read only)

Section 1 above was written from SKILL.md alone. After reading the base RULES block and the variants in the file, these corrections apply:
- Tokens for focus, pressed and disabled already exist (stroke-focus, radius-focus, focus-brand/plain/error, bg-*-pressed, bg-disabled, fg-disabled, opacity-disabled). What is missing is the variants that use them, not the tokens.
- A toast exists (ToastOverlay). Ad Slot has a loading state (rule 6.6). Neither needs a roadmap item.
- Rule 6.2 already covers button heights and touch targets, but says Button md (44) meets Material 48. It does not. Open question Q1 on the board.
- Rule sections 5 (auto layout) and 9 (canvas and annotation) are empty, so the board's two private parts (_Research/Cell, _Research/Card) are a first draft of annotation parts, not an approved pattern.
- The board is on page Research Interaction in the base file: state matrix, touch target table and six findings (F1-F4, Q1, Q2).

## 2. What the research says

Confidence: high = primary source read, medium = consistent across secondary sources, low = single or unverified source.

| Topic | Finding | Confidence |
|---|---|---|
| State set | NN/g: enabled, disabled, hover, focus, pressed are core. Add loading and selected (selected applies to checkbox/radio/tabs, not buttons). | high (NN/g read) |
| Focus | Never remove the focus indicator (WCAG). Use outline or stroke, not color alone. | high |
| Hover | Does not exist on touch. A mobile-first system should not rely on it. | high |
| Pressed | Must confirm the tap registered, within about 100-150 ms. | high (NN/g) |
| Loading | Keep the button's look, add a spinner, block double taps, keep width stable. | high (NN/g) |
| Response limits | 0.1 s: feels instant, no feedback needed. 1 s: flow holds, show that work is happening past this. 10 s: show percent progress and a way to cancel. | high (NN/g read) |
| Touch targets | Apple HIG Accessibility page: 44x44 pt. Material 3 accessibility page: at least 48x48 dp, and the target can extend beyond the visible element (a 24 dp icon sits in a 48 dp target). | high (both pages read) |
| Gestures | Do not clash with system edge gestures. Common actions get a visible button; swipes are shortcuts for content, never the only way. | medium |
| Haptics | Use sparingly: confirmations (purchase), errors, picker/switch ticks. | medium |
| Motion tokens | M3 durations: short1-4 = 50/100/150/200 ms, medium1-4 = 250-400 ms, long1-4 = 450-600 ms, extra-long 700-1000 ms. Easing: standard cubic-bezier(0.2, 0, 0, 1), standard decelerate (0, 0, 0, 1), standard accelerate (0.3, 0, 1, 1), emphasized decelerate (0.05, 0.7, 0.1, 1), emphasized accelerate (0.3, 0, 0.8, 0.15). Selection controls: 200 ms standard. Caveat from the page itself: M3 Expressive moved components to spring physics, and the easing and duration system is still valid for transitions but no longer maintained. Three-tier naming (primitive, semantic, component) and a reduced-motion override come from secondary sources. | high for values (page read in browser), medium for tiers |
| Tokens for agents | The W3C token format has duration and cubicBezier types, but a Google DESIGN.md issue says motion semantics are missing and agents invent defaults. Same gap we have. | low-medium (sources disagree) |
| Fitts / Hick | Big, well-spaced targets near the thumb; fewer choices per screen. Our "Choosing a part" and bottom nav already follow this. | medium |

## 3. Proposed changes, in priority order

Each one goes through the approval loop (proposal, preview on page Design, designer's OK, then build and log).

1. **State model rule (base).** One list of states and which parts get which. Core: enabled, pressed, focus, disabled. Extra only where the part needs it: loading (Button), selected (Tab, Checkbox, Radio, Switch, Chip), error (InputField). Drop hover for mobile. Each state differs by token, not by opacity (we already ban tint via opacity). Check which base parts have each state today and list the gaps in AUDIT.
2. **Touch target rule (base).** The base serves iOS (44 pt) and Android (48 dp). Recommend one shared minimum of 48 so one value fits both, held in a Dimension variable. The alternative is two values tied to the _Device collection, but _Device is not published, so tier 2 could not bind it. Decision for the designer. Done check gets a line: interactive nodes whose hit area is below the minimum, unless a larger hit area is documented. Icon buttons are the likely failures.
3. **Motion tokens (base).** Durations as Number variables, copied from the M3 values above (start with about four: 100, 200, 300, 500 ms). Easings: Figma now has native motion (keyframe easing with custom cubic-bezier, plus local custom animation styles saved in the file, from the figma-use-motion skill). So an easing can be a real curve on a style, not a string. Open question: those motion APIs are gated per user and custom styles may be gated separately, so test availability in the base file first (read only). If unavailable, fall back to String variables that code maps. Semantic names: feedback (pressed), enter, exit, emphasis. Reduced motion is a rule, not a mode: motion is optional, never carries meaning alone. Note that M3 Expressive uses springs now, so do not copy the old set blindly into a system meant to last.
4. **Interaction line in part descriptions.** Extend "Describing a part" with: Trigger, Response, Feedback, Time. Example: Button | tap | pressed fill, then action | pressed within 100 ms, loading if over 1 s. This gives agents a behavior spec without Figma prototyping.
5. **Loading, error and empty patterns (base).** Which part for which wait: under 1 s nothing, 1-10 s spinner or skeleton, over 10 s progress plus cancel. Errors: inline for fields, dialog only when blocking, always with the way out (we have "no dead ends" for flows, this is the same idea for states). Needs roadmap items for Skeleton and Toast/Snackbar if missing.
6. **Transitions between screens (flows rule).** Name the transition type on each arrow or jump tag: push, modal (bottom sheet, dialog), replace, tab switch. Apple and Material both separate these. Today an arrow says only "goes to".
7. **IAA/IAP interaction rules (base).** The app type we serve is where interaction design earns money and loses trust. Draft rules: rewarded ad always user-initiated and labeled before the tap; interstitial only at a natural break, never mid-task or right after a tap; paywall close control visible without delay and 44 pt; no fake-close or misplaced tap targets next to ads; confirmation and restore on purchase; limit-reached upsell offers a free way forward. Check each against Google Play and App Store policy text before it becomes a rule (not done yet).
8. **Gestures and haptics (later).** Only a short rule: no gesture-only actions, no edge swipes that clash with system back, haptics on purchase success and errors only.

## 4. Limits to keep in mind

- Figma Pro: no extended collections, so motion tokens live in the base and tier 2 mirrors them.
- Figma variables cannot hold easing curves, but native motion styles can (if enabled for the designer's account, not yet tested). Otherwise easings are strings that code maps.
- Prototype interactions (Smart Animate) can show motion, but agents read descriptions and variables better. Do the description and token work first, previews second.
- Nothing here is proven for our apps. Item 7 especially needs the designer's judgment and store policy.

## 5. Suggested first step

Do items 1, 2 and 4 together as one preview: a state matrix board on page Design for Button, InputField, Switch and Tab, with the touch target check run over the existing parts. It is cheap, visual, and shows the designer where the base already has the states and where it does not.

## Sources

- NN/g, Button states communicate interaction: https://www.nngroup.com/articles/button-states-communicate-interaction/
- NN/g, Response times: the 3 important limits: https://www.nngroup.com/articles/response-times-3-important-limits/
- UXPin, Button states: https://www.uxpin.com/studio/blog/button-states
- Material 3 easing and duration tokens (read in browser): https://m3.material.io/styles/motion/easing-and-duration/tokens-specs
- Material 3 accessibility, touch targets (read in browser): https://m3.material.io/foundations/designing/structure
- Apple HIG Accessibility, 44x44 pt (read in browser): https://developer.apple.com/design/human-interface-guidelines/accessibility
- Google DESIGN.md issue on missing motion tokens: https://github.com/google-labs-code/design.md/issues/47
- Haptics guidance is from secondary summaries only (Apple's "Playing haptics" page not read): https://designcode.io/ios-design-handbook-design-for-touch

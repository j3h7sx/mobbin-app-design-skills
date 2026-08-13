---
name: appllama-design-skill
description: Build native-feeling, benchmark-quality mobile app screens (Expo / React Native). Use when designing or implementing any mobile UI — screens, flows, onboarding, paywalls, tab bars, settings, empty states — or when polishing motion, typography, dark mode, or perceived performance. Enforces Apple HIG fidelity, semantic colors, native controls, purposeful Reanimated motion, a simulator-verified iteration loop, and a study-real-apps-first workflow (pairs with the Appllama MCP). Trigger on "build a screen", "make this screen better", "design the onboarding", "polish the UI", "make it feel native", or any mobile design/implementation task.
license: MIT
metadata:
  author: Appllama (appllama.io)
  version: 1.0.0
---

# Appllama Design Skill

You are building screens that will sit on a phone next to the best-designed apps
in the world. The user will compare your output to those apps within seconds of
launching it. This skill defines the bar and the method for clearing it.

## The Prime Directive: study before you draw

Never design a screen from imagination when you can study how top apps solved
the same screen. Real, shipping, revenue-ranked apps encode thousands of hours
of design iteration and A/B testing. Your first move on any screen is research:

1. If the **Appllama MCP** is connected, pull real screens for the category and
   screen type you are building (see the `appllama-usage` skill for the exact
   research playbooks). Study 20–30 screens before writing a line of UI code.
2. Extract the **pattern, not the pixels**: layout skeleton, information
   hierarchy, control choices, spacing rhythm, where the primary CTA sits, what
   gets an illustration vs. plain text, how progress is communicated.
   Note: every Appllama image and video carries a small Appllama watermark in
   the top-left corner. It is provenance, not design — ignore it when reading
   a screen (it may sit over the status bar or a back button) and never
   reproduce it in anything you build.
3. Then design **your** screen: same proven skeleton, your product's voice.
   Copying a competitor's screen 1:1 is both lazy and legally risky; shipping a
   screen that ignores every convention users already know is worse.

## Platform baseline

Default stack assumptions (override only if the project already differs):

- **Expo + Expo Router**, React Native, TypeScript.
- `react-native-reanimated` for motion, `react-native-gesture-handler` for
  gestures, `@shopify/flash-list` (or FlashList v2) for any list that can grow.
- `expo-image` for images (and SF Symbols via `source="sf:name"` on iOS),
  `expo-video` / `expo-audio` (never the deprecated `expo-av`).
- `react-native-safe-area-context` for insets. Never hard-code notch numbers.
- `process.env.EXPO_OS` over `Platform.OS` for compile-time platform checks.

## Native fidelity laws

These are the details that separate "web page in a wrapper" from "native app".
Violating any of them is a finding, not a style preference.

1. **Semantic colors, both themes, day one.** Use system/semantic color tokens
   (e.g. `Color` from `expo-router` on iOS: `Color.ios.label`,
   `Color.ios.secondarySystemBackground`; Material dynamic colors on Android).
   Every screen must render correctly in light AND dark before it is "done".
   Never pass semantic color objects into Reanimated animated styles — resolve
   to strings first.
2. **Native controls over rebuilt ones.** Switch, Slider, SegmentedControl,
   context menus, date pickers: use the native control or a faithful wrapper.
   A rebuilt toggle that animates 50 ms differently than iOS's reads as fake
   instantly.
3. **SF Symbols / Material Symbols for iconography.** On iOS prefer SF Symbols
   (`expo-image` with `sf:` sources, or `expo-symbols`); they inherit weight,
   optical size, and Dynamic Type behavior. Do not mix three icon families on
   one screen.
4. **Typography is hierarchy.** Use the platform type ramp (Large Title / Title
   / Headline / Body / Footnote on iOS). One display size per screen. Tabular
   numerals (`fontVariant: ['tabular-nums']`) for anything that counts, times,
   or prices. `Text selectable` on data users may want to copy.
5. **Continuous corners.** `borderCurve: 'continuous'` on every rounded
   rectangle. Squircles are the single cheapest "feels iOS" win that exists.
6. **Shadows via CSS `boxShadow`**, not legacy `shadow*`/`elevation` props.
   Shadows are for elevation logic, not decoration — one elevation system per
   app.
7. **Spacing rhythm.** Pick a base unit (4 or 8) and never leave it. Prefer
   flexbox `gap` over margin stacking. ScrollView padding goes in
   `contentContainerStyle`, never on the ScrollView itself.
8. **Safe areas and the Dynamic Island are part of the design.** Screens must
   be verified with content scrolled under the island / status bar (does the
   blur/fade treatment hold?), with the home indicator (does the bottom CTA
   clear it?), and in landscape if supported.
9. **Navigation titles belong to the navigator.** Use the stack's native title
   (and large-title collapse behavior on iOS) rather than a hand-rolled header
   whenever possible.
10. **Haptics are punctuation.** Light impact on selection/confirm on iOS,
    success/warning notifications for outcomes. Never on scroll, never in
    loops. Guard with platform checks.
11. **Format numbers like a product, not a database**: 1.4M, 38k, $4.99. Trim
    trailing zeros. Localize dates.
12. **Root scroll behavior**: screens that can ever overflow wrap content in a
    ScrollView (first component in the route) with
    `contentInsetAdjustmentBehavior="automatic"`. Use `useWindowDimensions`,
    never `Dimensions.get()`.

## Motion laws

Motion is the highest-leverage polish surface and the easiest to overdo.

- **Every animation needs a reason**: continuity (element moves between
  states), causality (response to a gesture), or orientation (where did this
  come from). Decoration-only motion gets cut.
- **Reanimated worklets on the UI thread** for anything tracking a gesture.
  Gesture → animation must never hop the JS thread.
- **Springs over durations** for anything the user "touches"; gentle
  timing curves (250–350 ms, ease-out) for anything the system initiates.
- **Entering/exiting animations** (`FadeIn`, `SlideInDown`, layout transitions)
  on list items, modals, and conditional content — subtle, 150–250 ms.
- **Respect Reduce Motion.** Query the accessibility setting and collapse
  spatial animations to cross-fades.
- The bar to hit: 60 fps on a mid-tier device, zero dropped frames during the
  hero transition of your flow. Measure, don't vibe — see
  [references/performance.md](references/performance.md).

## State architecture

Screens that feel great are screens whose state is boring:

- **Server state** in TanStack Query (or the project's equivalent): caching,
  retries, optimistic updates. Never `useEffect`+`fetch`.
- **Client state** in a small atomic store (Zustand/Jotai). Broad "app state"
  contexts cause the re-render cascades that make UIs feel heavy.
- **Ephemeral UI state** (open/closed, focus, scroll) stays local to the
  component.
- **Optimistic by default**: taps reflect instantly, reconcile in the
  background, roll back loudly on failure.
- Uncontrolled `TextInput`s for high-frequency typing surfaces; controlled
  inputs are a top-3 cause of typing jank.
- Persist tiny client state in MMKV, not AsyncStorage, when latency shows.

## Perceived performance

- Skeletons only for content whose shape you know; otherwise progressive
  reveal. Never a full-screen spinner for a partial update.
- FlashList for every list; give stable keys.
- Preload the next screen's data on press-in, not on navigation-complete.
- Images: right-size sources, `expo-image` with `recyclingKey` in lists,
  thumbhash/blurhash placeholders.
- Cold-start TTI and bundle discipline live in
  [references/performance.md](references/performance.md) — apply the
  measure → optimize → re-measure loop, never blind memoization.

## Image & illustration assets

When a screen calls for illustration, empty-state art, hero imagery, or icons
beyond the symbol set:

- Generate assets with the **best image model available to you** (e.g. an
  imagegen tool or the Higgsfield MCP/CLI if connected) at the **highest
  quality settings**, then downscale to @1x/@2x/@3x. Never upscale.
- One visual language per app: pick a style (gradient-mesh, flat-duotone,
  3D-clay, hand-drawn, mascot style) and generate ALL assets in that same style, same
  palette, same lighting. A mixed-style asset set reads as template slop.
- Prompt for **transparent or solid-flat backgrounds** matched to your surface
  color; composite artifacts (white halos, wrong-color mattes) are an
  automatic redo.
- Full asset pipeline and prompt patterns:
  [references/image-assets.md](references/image-assets.md).

## The simulator loop (non-negotiable)

A screen does not exist until you have seen it running. The loop:

1. Implement → launch in the iOS Simulator (or Android emulator).
2. Screenshot and **actually look**: alignment, optical centering, spacing
   rhythm, truncation with long content, dark mode, Dynamic Type at XL.
3. Exercise the motion: record, scrub frame by frame if a transition looks
   off. Watch content pass under the Dynamic Island and behind the tab bar.
4. Fix, relaunch, re-verify. Repeat until you cannot find a defect — then run
   the checklist in [references/simulator-loop.md](references/simulator-loop.md)
   once more.

Do not declare a screen finished from code review alone. Do not stop at "looks
fine" — stop at "cannot find a flaw at 100% zoom".

## Definition of done, per screen

- [ ] Studied 10+ real reference screens for this screen type (via Appllama
      MCP when available) and can name the pattern you adopted
- [ ] Light + dark mode verified in the simulator
- [ ] Safe areas / Dynamic Island / home indicator verified
- [ ] Long-content, empty, loading, and error states designed — not defaulted
- [ ] Motion: entrances, presses, and transitions feel native; Reduce Motion
      respected; 60 fps measured on the target device profile
- [ ] Dynamic Type XL doesn't break layout; text is selectable where useful
- [ ] All tap targets ≥ 44pt; contrast passes in both themes
- [ ] Assets: single style family, crisp at @3x, no compositing halos
- [ ] List surfaces virtualized; no controlled-input jank; no re-render storms
      (profiled, not guessed)

## References

| File | Load when |
|---|---|
| [references/native-controls.md](references/native-controls.md) | Choosing/wiring iOS+Android native controls, menus, pickers, sheets |
| [references/motion.md](references/motion.md) | Any Reanimated work: gestures, transitions, springs, layout animations |
| [references/performance.md](references/performance.md) | Jank, slow TTI, big bundles, memory leaks, profiling method |
| [references/image-assets.md](references/image-assets.md) | Generating illustrations/icons/hero art with image models |
| [references/simulator-loop.md](references/simulator-loop.md) | Final verification checklist + device matrix |

---
name: mobbin-app-design-skill
description: >-
  Build native-feeling, benchmark-quality mobile app screens with Expo and
  React Native. Use when designing or implementing mobile screens, flows,
  onboarding, paywalls, navigation, tabs, sheets, settings, empty states, or
  when polishing typography, motion, dark mode, perceived performance, and
  native platform behavior. Uses Mobbin research before implementation and a
  simulator-verified iteration loop afterward.
license: MIT
metadata:
  version: 1.0.0
---

# Mobbin App Design Skill

Build screens that can sit beside the best-designed shipped apps without
feeling generic, web-like, or unfinished. This skill defines the implementation
bar and the method for reaching it.

## Prime directive: study before drawing

Do not design from memory when real references can answer the question.

1. If Mobbin MCP is connected, use `mobbin-usage` to research the relevant
   screen type and surrounding flow before writing UI code. Inspect enough
   images to reach pattern saturation; for a substantial new screen, this is
   usually at least 10 strong references and often 20–30.
2. Extract the pattern, not the pixels: layout skeleton, information hierarchy,
   control choices, spacing rhythm, navigation presentation, CTA placement,
   illustration role, progress treatment, and state transitions.
3. Preserve each reference's canonical `mobbin_url` and cite the references
   that materially shaped the result. Mobbin image URLs expire; the canonical
   links and IDs are the durable evidence.
4. Design the product's own screen using proven conventions and its existing
   brand voice. Do not copy another product one-to-one.

## Platform baseline

Respect the existing project stack. When starting from an unconstrained Expo
project, prefer:

- Expo Router, React Native, and TypeScript.
- `react-native-reanimated` for motion and
  `react-native-gesture-handler` for gestures.
- FlashList for lists that can grow.
- `expo-image` for images and supported iOS symbols; `expo-video` and
  `expo-audio` instead of deprecated media packages.
- `react-native-safe-area-context` for insets. Never hard-code notch values.
- Compile-time platform checks when available; otherwise use the project's
  established platform abstraction.

Also load `vercel-react-native-skills`, `react-native-best-practices`,
`animate`, and `uniwind` when their triggers match the work.

## Native fidelity laws

These are functional quality requirements, not decorative preferences.

1. **Semantic colors in every supported theme.** Use system or design-system
   roles rather than scattered literals. Verify light and dark themes before
   calling a screen done. Resolve semantic color objects to strings before
   sending them into animated styles.
2. **Native controls first.** Use platform controls or faithful wrappers for
   switches, sliders, segmented controls, menus, date pickers, and system
   pickers. Rebuild only when the product genuinely needs different behavior.
3. **One coherent icon system.** Prefer SF Symbols on iOS and Material Symbols
   on Android where appropriate. Match weight and optical size; do not mix
   unrelated icon families on one screen.
4. **Typography creates hierarchy.** Use the platform or product type ramp.
   Keep one dominant display size per screen. Use tabular numerals for counts,
   times, and prices. Make useful data selectable.
5. **Continuous corners.** Use `borderCurve: "continuous"` where supported and
   keep every radius on a declared scale.
6. **Shadows communicate elevation.** Use the project's supported shadow API
   and one elevation system. Avoid decorative shadow noise.
7. **Spacing follows one rhythm.** Use a four- or eight-point base and flexbox
   `gap` where practical. Put ScrollView padding in
   `contentContainerStyle`, not on the ScrollView itself.
8. **Safe areas are part of the design.** Verify the status bar or Dynamic
   Island, the home indicator, scrolled-under headers, and landscape if the app
   supports it.
9. **Navigation titles belong to navigation.** Prefer the navigator's native
   title and large-title behavior instead of rebuilding a header.
10. **Haptics are punctuation.** Pair appropriate selection, impact, success,
    or error haptics with visible feedback on the same frame. Emit at most one
    haptic per action; never vibrate continuously or during scrolling.
11. **Format values for people.** Compact large numbers where appropriate,
    trim meaningless trailing zeros, and localize dates, currencies, and units.
12. **Root scrolling is resilient.** A route that can overflow should begin
    with a scroll container or virtualized list and use automatic inset
    adjustment where supported. Use `useWindowDimensions`, not a static screen
    measurement.

## Navigation laws

Every transition must answer: what is the destination relative to the current
screen, should the user be able to return, and what does Back do afterward?

1. **Push goes deeper; replace moves on.** Push when returning is meaningful.
   Replace or redirect after a state-changing one-way transition. Dismiss a
   completed modal flow to its intended destination. Back undoes navigation,
   never real-world events.
2. **Presentation is meaning.** A self-contained multi-step task is a modal
   with its own stack. A short interruption is a form sheet or bottom sheet.
   Immersive content is a full-screen modal. Content floating above a still
   visible screen is an overlay. Destructive confirmation is an action sheet or
   platform dialog. Sharing, browsing, photos, and documents use system
   controllers. If a sheet grows a second step, it was probably a modal; if a
   link can open it, it is a route rather than local boolean state.
3. **One-way doors leave the stack.** Completed sign-in, onboarding, purchase,
   or sessions must not be reachable by Back. Guard routes and replace the
   obsolete stack state. Preserve context when auth or purchase was requested
   from a feature: dismiss back to that feature and complete the intended
   action there.
4. **Block Back only for real risk.** Prevent removal only while an irreversible
   request is in flight, or when a modal contains unsaved work and the user is
   asked first. Transient in-screen state may consume the first Back action;
   otherwise edge swipe and system Back remain available.
5. **Tabs are peers.** Do not slide between tabs. Preserve each tab's stack and
   make re-tapping the active tab return to its root. Full-attention screens
   live above the tab navigator. Deep links should build a meaningful stack
   beneath the destination, and cold start should wait for session state rather
   than flashing the wrong route.
6. **Study grammar as well as pixels.** When inspecting Mobbin flows, determine
   whether each step is a push, modal, sheet, overlay, tab root, or replacement.
   Carry the winning flow's consistency into the navigation specification.

## Anti-slop laws

These are default bans. Override them only when the brand explicitly requires
the treatment and the choice fits the product.

1. **No model-default styling.** Avoid reflexive purple gradients, glowing
   CTAs, glass on every card, generic mesh heroes, decorative sparkles, and
   confetti for minor events. Derive the visual language from the product and
   the Mobbin references.
2. **One accent, locked.** Use one accent color consistently for primary
   actions, active states, and progress.
3. **One neutral family.** Choose warm or cool neutrals and stay consistent.
4. **Lock the shape scale.** State the radii for actions, cards, inputs, and
   sheets; do not introduce arbitrary new radii.
5. **No emoji as interface chrome.** Use the platform icon system. Emoji may
   appear sparingly as content when the product voice genuinely calls for it.
6. **One label per intent.** Use the same wording for the same action across
   every screen.
7. **Emphasis stays in the type family.** Use weight, italic, size, or color;
   do not swap typefaces inside a headline merely for visual interest.
8. **Ship complete state cycles.** Design loading, empty, error, offline,
   success, and returning states—not only the populated happy path.
9. **Run a mechanical preflight.** Count accent hues, radii outside the scale,
   emoji in chrome, unjustified gradients, and duplicate labels. Fix every
   violation before the simulator pass.

## Motion laws

Decide whether motion is justified before implementing it.

- **Frequency gate.** Interactions seen constantly use platform defaults.
  Frequent press and selection feedback stays nearly imperceptible and under
  150 ms. Sheets, modals, and toasts use standard motion. Delight belongs only
  to rare or first-time moments. Tabs never slide; screen transitions remain
  native.
- **Name one purpose:** feedback, spatial continuity, state change, preventing
  a jarring cut, explanation, or delight. If no purpose applies, omit motion.
- **Gesture-driven motion uses a spring.** Start from the live value, pass
  release velocity, choose the target from projected momentum, rubber-band at
  boundaries, and keep the object interruptible mid-flight. Define one spring
  vocabulary for the app.
- **System-driven motion uses timing.** Keep it under 300 ms with a strong
  ease-out. Press feedback begins on press-in. Exits are faster than entrances
  and reverse the entrance direction. Do not enter from zero scale.
- **Keep gestures on the UI thread.** Use worklets and shared values for the hot
  path; cross to JavaScript only at the end for navigation or effects. Prefer
  transforms and opacity, avoid height animation, and track the keyboard with a
  native-synchronized controller rather than guessed durations.
- **Respect Reduce Motion.** Spatial effects collapse to cross-fades while
  native system transitions remain native.
- **Measure the result.** Hold 60 fps through the hero flow on a release build
  and the slowest supported device. Read
  [references/motion.md](references/motion.md) and
  [references/performance.md](references/performance.md) for implementation and
  profiling details.

## State architecture

- Keep server state in the project's query/cache layer rather than ad hoc
  effect-driven requests.
- Keep shared client state in focused stores or atoms; avoid broad contexts
  that re-render unrelated leaves.
- Keep ephemeral UI state—focus, local disclosure, and scroll—inside the
  owning component.
- Reflect safe actions immediately, reconcile in the background, and roll back
  visibly on failure.
- Avoid forcing high-frequency text input through a large controlled render
  tree. Choose controlled or uncontrolled input based on validation and
  performance requirements, then profile the actual typing path.
- Persist only small, appropriate client state and use the project's established
  storage layer.

## Perceived performance

- Use skeletons only when the final shape is known; otherwise reveal content
  progressively. Do not block an entire screen for a partial update.
- Virtualize growable lists and use stable keys.
- Prefetch the next screen's data before navigation completes when the intent
  is sufficiently clear and the request is safe.
- Right-size images, use `expo-image` in Expo projects, provide placeholders,
  and set recycling identifiers in reused list cells.
- Measure cold-start time, render commits, memory, bundle growth, and frame rate
  before choosing an optimization. See
  [references/performance.md](references/performance.md).

## Image and illustration assets

When a screen genuinely needs illustration, empty-state art, hero imagery, or
icons beyond the platform symbol set:

- Use the best available image-generation capability at high quality, then
  downscale for delivery. Never upscale a small source.
- Define one style, palette, lighting model, and subject grammar for the whole
  product. Regenerate outliers rather than shipping mixed styles.
- Request transparent or exact solid backgrounds and inspect edges for halos,
  matte fringes, and compression artifacts.
- Follow [references/image-assets.md](references/image-assets.md) for the full
  pipeline and quality gate.

## Simulator loop

A screen does not exist until it has been inspected while running.

1. Implement and launch the iOS Simulator or Android emulator.
2. Capture and inspect the screen at full size for alignment, optical centering,
   rhythm, truncation, theme behavior, safe areas, and enlarged text.
3. Record the complete flow and exercise transitions, Back behavior, one-way
   doors, sheets, modals, keyboard movement, press states, gestures, rapid taps,
   and scroll extremes.
4. Watch once at normal speed and again frame by frame. Look for dropped frames,
   wrong-theme flashes, unstyled first paints, layout jumps, clipped springs,
   and double-render pops.
5. Fix, relaunch, and verify again. Finish with
   [references/simulator-loop.md](references/simulator-loop.md).

Do not declare completion from code review alone. Stop only when the running
flow has no meaningful visual, motion, navigation, state, or accessibility
defect.

## Definition of done

- [ ] Studied at least 10 relevant Mobbin screens for a substantial screen type,
      or documented why fewer references reached saturation, and named the
      pattern adopted.
- [ ] Linked every decisive Mobbin reference with its canonical URL.
- [ ] Defined whether the screen is a push, modal, sheet, overlay, tab root, or
      replacement; verified iOS and Android Back behavior and one-way doors.
- [ ] Verified every supported theme in the simulator or emulator.
- [ ] Verified safe areas, status bar or Dynamic Island, and home indicator.
- [ ] Designed and forced long-content, empty, loading, error, offline, and
      success states as applicable.
- [ ] Recorded and inspected the complete flow, including keyboard and gesture
      transitions; respected Reduce Motion; measured release-build performance.
- [ ] Verified enlarged text, contrast, and tap targets of at least 44 points.
- [ ] Kept assets in one crisp, artifact-free style family.
- [ ] Virtualized growable lists and profiled suspected input or render jank.

## References

| File | Load when |
|---|---|
| [references/native-controls.md](references/native-controls.md) | Choosing and wiring native controls, menus, pickers, forms, and sheets. |
| [references/motion.md](references/motion.md) | Implementing Reanimated gestures, transitions, springs, and layout motion. |
| [references/performance.md](references/performance.md) | Diagnosing frame drops, slow startup, bundle growth, typing lag, or memory leaks. |
| [references/image-assets.md](references/image-assets.md) | Generating and preparing illustrations, icons, or hero art. |
| [references/simulator-loop.md](references/simulator-loop.md) | Performing the final device, state, accessibility, and motion verification. |

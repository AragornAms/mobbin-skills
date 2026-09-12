# Performance — measure, fix, and re-measure

Perceived quality depends on responsiveness as much as visual design. Do not
optimize from intuition alone.

## The loop

1. Measure a baseline for the exact interaction: frame rate during a transition,
   cold-start time, input latency, render commits, or memory after repeated
   navigation.
2. Change the single cause supported by the evidence.
3. Repeat the same measurement under the same conditions.
4. Report the observed before and after values. Without comparable measurements,
   describe the change but do not claim a performance improvement.

Do not add memoization without evidence of repeated expensive work. Do not flag
a theoretical closure or render problem without a reproduction or profile.

## Frame rate and re-renders

- Replace growable ScrollView-rendered collections with a virtualized list such
  as FlashList.
- Profile suspected render storms. Common causes include broad contexts or
  stores consumed by leaves, unstable object props passed to memoized children,
  and parent state that belongs near the affected component.
- Use focused selectors or atoms so updates reach only their consumers.
- Use React Compiler or manual memoization only where the project's setup and
  profiling justify it.
- Use deferred rendering for expensive derived UI behind fast-changing input
  when that preserves correctness.

## Typing

Keep the smallest possible subtree on the per-keystroke path. Controlled input
is appropriate when the rendered value must be authoritative; uncontrolled or
locally buffered input can be better for high-frequency search and large forms.
Choose deliberately and profile on a representative device.

## Startup and time to interactive

- Measure cold starts on release builds.
- Keep native screen optimizations enabled.
- Defer SDK initialization, analytics, and below-the-fold work that first paint
  does not require.
- Inspect bundle composition after meaningful growth. Avoid broad barrel imports
  that pull unnecessary modules into the initial bundle.
- Confirm the current Hermes and React Native recommendations for the project's
  versions before applying engine-level tuning.

## Memory

- Repeatedly navigate through the suspected flow and watch whether memory returns
  toward baseline.
- Use heap snapshots to find retained listeners, timers, subscriptions, and
  closures before blaming native modules.
- Give recycled images stable recycling identities and avoid capturing large
  parent scopes in list-item callbacks.

## Animation-specific checks

- Confirm continuous gestures run as worklets and do not cross to JavaScript on
  every frame.
- Defer expensive destination work until the navigation transition completes if
  profiling shows that render commit causing the hitch.
- Check image decode and first-render cost before retuning an otherwise healthy
  motion curve.

## Target budgets

Treat these as starting targets and tighten them for the product and supported
hardware:

| Metric | Initial target |
|---|---|
| Transition and gesture frame rate | Sustained device refresh rate; at least 60 fps on the supported baseline |
| Cold-start time to interactive | Under 2 seconds on a representative mid-tier device when feasible |
| Keystroke to visible echo | Under 50 ms |
| Virtualized list fling | No visible blank cells or repeated decode flashes |
| Initial bundle | Investigate unexpected growth around 10% or more |

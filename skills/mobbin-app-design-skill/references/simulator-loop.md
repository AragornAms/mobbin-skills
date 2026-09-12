# Simulator loop — verification checklist and device matrix

A screen is finished when it survives inspection in a real simulator or
emulator, not when it compiles.

## Loop mechanics

1. Launch the project's development or release build in the primary iOS
   Simulator. Verify Android in its emulator as well when supported.
2. Capture the screen and inspect the actual image. Check alignment, clipping,
   hierarchy, text wrapping, state, and optical centering rather than relying on
   memory of the code.
3. Interact with every control, enter long content, background and foreground
   the app, rotate when supported, and force non-happy states.
4. Record the complete flow. Watch it once at full speed for feel and once frame
   by frame for flashes, jumps, interrupted motion, and dropped frames.
5. Fix a small set of defects, relaunch, and repeat. Large unverified batches
   make regressions difficult to isolate.
6. When a UI automation tool is already available, capture the stable happy
   path with assertions and screenshots so later changes can repeat it.

## Per-screen checklist

### Layout

- [ ] Content clears or intentionally travels beneath the status bar and
      Dynamic Island without a hard unintended edge.
- [ ] Bottom actions clear the home indicator and system navigation regions.
- [ ] Icons, text baselines, centers, and perceived visual weight align.
- [ ] Spacing follows the declared rhythm and radius scale.
- [ ] Long titles, translations, and large values wrap or truncate by design.
- [ ] Empty, loading, error, offline, success, and returning states have been
      forced and inspected when relevant.

### Theme and type

- [ ] Every supported theme has been captured and inspected.
- [ ] Enlarged text does not overlap, clip, or hide required actions.
- [ ] Text reflows in a sensible reading order.
- [ ] Primary and secondary content meets contrast requirements in every theme.

### Motion

- [ ] First-mount entrances play only when appropriate and do not replay after
      ordinary Back navigation.
- [ ] Gestures track the finger continuously, release with velocity, and settle
      cleanly after cancellation or interruption.
- [ ] No first-paint flash, wrong-theme frame, color pop, double-render jump, or
      clipped overshoot appears in the recording.
- [ ] Every sheet and modal is recorded presenting, dragging, cancelling, and
      dismissing.
- [ ] Keyboard appearance and dismissal move the layout continuously and keep
      the focused field visible.
- [ ] Performance sustains the supported device refresh target through every
      transition, measured on a release build.
- [ ] Reduce Motion converts spatial effects to non-spatial alternatives.

### Interaction

- [ ] Tap targets are at least 44 points where platform guidance calls for it.
- [ ] Pressed, selected, focused, disabled, and destructive states are clear.
- [ ] Haptics accompany rather than replace visible feedback.
- [ ] The keyboard type, autofill, Return-key behavior, and dismissal are useful.
- [ ] iOS edge swipe and Android system Back work everywhere they should.
- [ ] Rapid taps cannot double-navigate, duplicate payment, or submit twice.

### State and lifecycle

- [ ] Backgrounding and returning preserve the correct durable state.
- [ ] Killing and relaunching restore persisted state and reset ephemeral state.
- [ ] Offline and failed actions queue safely or fail visibly.
- [ ] Completed one-way transitions cannot be re-entered with Back.
- [ ] Authentication or purchase launched from a feature returns to that feature
      and completes or clearly resumes the original intent.

## Minimum device matrix

| Profile | Purpose |
|---|---|
| Current iPhone Pro class | Primary iOS design, Dynamic Island, current metrics |
| Small iPhone or SE class | Compression, text growth, and action reachability |
| Representative current Pixel | Material behavior, Back navigation, Android font metrics |
| Tablet or iPad when supported | Responsive structure, split layouts, and orientation |

Run the full checklist on the primary target. On secondary devices, at minimum
verify layout, safe areas, enlarged text, Back behavior, and the decisive flow.

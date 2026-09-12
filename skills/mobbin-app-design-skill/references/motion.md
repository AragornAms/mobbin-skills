# Motion — Reanimated patterns that feel native

Use this reference for gesture-driven and system-driven animation. Motion must
clarify interaction without delaying the user or competing with content.

## Two motion families

| Family | Driver | Typical curve | Examples |
|---|---|---|---|
| Responsive | Finger position and velocity | Interruptible spring seeded with velocity | Sheet drag, swipe-to-dismiss, card pan |
| Narrative | Application state and time | Short timing curve with strong ease-out | Entrances, fades, reveals, toasts |

Do not close a flung sheet with a fixed-duration animation, and do not turn
frequent button feedback into a long, playful spring.

## Springs

Define one shared spring vocabulary for the app. A useful starting point is a
critically damped settle for ordinary movement and a slightly softer response
for rare celebratory motion:

```ts
const SNAP = { duration: 400, dampingRatio: 1 };
const POP = { duration: 400, dampingRatio: 0.8 };

offset.set(withSpring(destination, {
  ...SNAP,
  velocity: event.velocityY,
}));
```

- Pass gesture velocity into the release spring.
- Choose destinations from both distance and velocity so a short, fast flick
  can commit.
- Let a new gesture grab the current animated value mid-flight.
- Use bounce only when the gesture or product language earns it.

## Keep gesture updates on the UI thread

```ts
const pan = Gesture.Pan()
  .onChange((event) => {
    offset.set(offset.get() + event.changeY);
  })
  .onEnd((event) => {
    const dismiss = offset.get() > height * 0.3 || event.velocityY > 800;
    offset.set(
      withSpring(dismiss ? height : 0, {
        ...SNAP,
        velocity: event.velocityY,
      }),
    );

    if (dismiss) scheduleOnRN(onClose);
  });
```

- Do not read or write React state from the continuous gesture callback.
- Cross to JavaScript only when navigation or an external effect must occur.
- Use the APIs supported by the installed Reanimated/worklets versions; do not
  paste a newer API into an older project without checking.
- Avoid allocating arrays and objects in hot per-frame code.

## Entrances, exits, and layout

- Use subtle entrance motion only when it prevents a jarring cut or explains
  where content came from.
- Keep exits about 30% faster than entrances.
- Stagger a short group only; after roughly eight items, reveal the remainder as
  a block.
- Apply layout transitions to containers whose children reorder or resize.
- Preserve perceived object continuity by matching thumbnail position, aspect
  ratio, and corner radius between origin and destination.
- Never replay first-mount choreography merely because the user navigated back.

## Scroll-linked behavior

- Drive effects from native scroll offsets.
- Keep headers at a fixed layout height and animate content inside a clipped
  container instead of animating the header's height every frame.
- Clamp normal ranges and define intentional overscroll behavior.
- Reproduce familiar patterns precisely: collapsing titles, translucent bars,
  and restrained hero-image stretch.

## Reduce Motion

Every spatial animation needs a non-spatial fallback. Replace translations,
large scaling, parallax, and shared-space movement with a short cross-fade when
Reduce Motion is enabled. Keep system-owned transitions under system control.

## Performance guardrails

- Prefer `transform` and `opacity`; layout properties can force work each frame.
- Keep animated styles focused on their own nodes.
- Avoid mount animations on recycled list rows.
- Synchronize keyboard-following UI with a native keyboard controller.
- Profile a stutter before changing springs. Common causes are heavy renders
  committed during the transition and image decoding on a critical thread.

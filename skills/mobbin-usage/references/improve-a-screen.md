# Playbook: make an existing screen or section better

Use this playbook when the user provides code, a screenshot, or a running
product and asks to improve it. "Better" means a concrete improvement in
hierarchy, clarity, interaction, accessibility, and platform fit, supported by
real comparative references and verified in the running product.

## 1. Diagnose before searching

Run or inspect the existing surface first. Name the three most important
deficits precisely, such as competing primary actions, unclear grouping,
missing state feedback, weak touch targets, or a transition that does not match
the navigation model. Each Mobbin search should answer one of these diagnosed
questions; do not search for generic inspiration.

## 2. Build a broad and focused reference board

Run complementary `search_screens` passes:

- A literal pass describing the screen type, visible content, and important
  controls. Use `mode="standard"` when a fast direct match is enough.
- An intent-rich pass describing the desired information relationship and user
  task. Use `mode="deep"` for nuanced matching.

For website modules, use the same broad/focused split with `search_sections`.
For a surface that belongs to a journey, also use `search_flows` to understand
the steps immediately before and after it.

Keep `task_intent` identical across calls. On additional screen passes, use
`exclude_screen_ids` and sharpen the query so results add evidence instead of
repeating it. For flows and sections, advance `page` while
`has_next_page=true`. Ask for manageable batches, inspect every returned image,
and stop when new references no longer change the target specification.

Save useful references in the local research structure, including each ID and
canonical `mobbin_url`. Select the strongest five to eight and state what each
one proves. Do not select on visual polish alone; prefer references that solve
the diagnosed problem.

## 3. Extract a checkable target

From the selected references, write a compact specification covering:

- layout skeleton and grouping;
- information hierarchy and reading order;
- control choices, labels, and interaction feedback;
- spacing and typography rhythm;
- semantic color roles in supported themes;
- entrance, press, state-change, and exit motion;
- empty, loading, error, success, and edge states;
- accessibility and responsive behavior.

Every line should be observable in a screenshot, interaction, or accessibility
check. Link each reference used to its `mobbin_url`.

## 4. Rebuild and iterate

1. Implement against the specification using `mobbin-app-design-skill` for
   mobile work or `frontend-design` for web work, plus any platform, animation,
   and performance skills those implementations require.
2. Generate or source missing imagery only when it serves the screen's job, and
   keep it consistent with the product's visual system.
3. Run the actual app or site, capture the result, and compare it side by side
   with the strongest references. Exercise transitions and interactive states,
   fix the gaps, and repeat.
4. Verify small and large sizes, light and dark themes where supported, safe
   areas, enlarged text, reduced motion, keyboard behavior, and smooth feedback.
5. Stop when the revised surface meets the specification and no meaningful
   comparison gap remains—not merely when it is better than before.

## 5. Verify the surrounding flow

After the surface passes, walk at least one step before and one step after it.
Check entrance and exit transitions, state carried across boundaries, and Back
behavior on every supported platform. If the surface is a sheet, modal, nested
step, or sits behind a one-way transition, verify that its presentation matches
its role in the journey. Use `search_flows` when the surrounding pattern needs
more evidence.

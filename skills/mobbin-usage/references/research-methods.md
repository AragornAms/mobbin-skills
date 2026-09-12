# Research methods: flows, components, and website sections

## Flow research — study journeys, not isolated screenshots

Use flows when the question is "How do shipped products structure this user
journey?" rather than "What does this one screen look like?"

1. Call `search_flows` with one journey described in plain language, such as
   "onboarding with symptom personalization and notification permission
   timing" or "checkout with delivery selection and Apple Pay."
2. Set `platform` explicitly. Keep the task's `task_intent` unchanged across
   every call. Name an app in the query only when you intentionally want that
   app's version.
3. Inspect the preview images for every screen in every returned flow. The
   ordered screens reveal step count, what each step asks and gives, where
   friction appears, how progress is communicated, and whether a step behaves
   like a push, sheet, modal, overlay, or root.
4. Advance the 1-based `page` while `has_next_page=true` and new results still
   affect the specification. Flow pages cap at 20.
5. Compare three to five strong journeys side by side and chart their common
   spine, meaningful differences, and surrounding state transitions.

High-value studies include first run, onboarding, sign-up, permission timing,
checkout, upgrade or paywall, search, creation, sharing, cancellation, and the
category's signature task.

## Component research — study one design decision

When the question is component-level, use `search_screens` and describe the
component in context rather than submitting a keyword list. Examples:

- "medication dashboard with a bottom tab bar, centered add action, and a
  visible selected state";
- "weekly progress card with completed days, missed days, and a details link";
- "notification permission primer with benefit bullets before the system
  prompt."

Run `mode="standard"` for direct literal matches and `mode="deep"` when the
relationship or intent matters. Use `exclude_screen_ids` for a non-repeating
second pass. Inspect every image, then extract measurable choices: placement,
size relationships, number of items, icon and label conventions, active and
disabled states, feedback, and interaction affordances. Always preserve and
cite each screen's `mobbin_url`.

## Website-section research

Use `search_sections` for a page module such as a hero, feature grid, pricing
comparison, testimonial block, FAQ, footer, or navigation header. Search one
section per query, inspect the returned images, and page sequentially until the
evidence saturates. Extract the content order, responsive structure, CTA
hierarchy, trust signals, and relationship to neighboring sections.

Use `search_screens(platform="web")` when the question concerns a complete web
app screen or application state. Use `search_sections` when the question
concerns a constituent website section.

## Study discipline

- **Question first.** Every search answers a named decision in the current
  task. A collection of attractive images without a question is not research.
- **Pixels before metadata.** Screen names, app names, action labels, and counts
  help organize results; they do not prove what the UI contains. Inspect the
  returned images directly.
- **Journey before snapshot.** When a screen belongs to a multi-step experience,
  study the surrounding flow and state transitions.
- **Cross-product before single-product.** One product shows one taste. Several
  strong, relevant products reveal conventions, real choices, and category
  grammar.
- **Do not invent performance evidence.** Mobbin MCP results do not supply
  revenue, downloads, ratings, conversion, or retention. Call a pattern common,
  clear, or well suited to the task when the evidence supports that claim; do
  not call it higher-converting without separate evidence.
- **Cite the evidence.** Link every specific Mobbin reference to its canonical
  `mobbin_url` in notes and user-facing findings.
- **Stop at saturation.** Continue while new references change the
  specification. Stop when they only repeat already-understood patterns.
- **Preserve durable identifiers.** Image URLs expire after 30 days. Keep the
  screen or flow ID, app or site name, and canonical Mobbin URL beside every
  useful observation.

## Working with user-curated references

If the user provides a Mobbin screen, flow, or collection link, treat it as a
requirement and start there. Inspect it with an available browser or web-reading
tool when possible, record its canonical link, and then use the MCP searches to
find supporting or contrasting references. Do not pretend a board-reading or
ID-lookup tool exists unless it is actually available in the current runtime.

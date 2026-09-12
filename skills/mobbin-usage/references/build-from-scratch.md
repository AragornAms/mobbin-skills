# Playbook: build from scratch

Use this playbook when the user asks for a new app, website, feature, or product
flow. The outcome is a finished experience whose important screens and states
have been compared with real references in the running product, not a scaffold
or a detached mood board.

## Phase 1 — Find the relevant products and journeys

1. Translate the brief into two or three named research questions. Search the
   category's defining journeys with `search_flows`, decisive surfaces with
   `search_screens`, and website-only modules with `search_sections`.
2. Keep the same concise `task_intent` across calls. Put the target platform in
   the `platform` field and search one screen, flow, or section per query.
3. Shortlist roughly five products by relevance to the brief, quality of the
   returned evidence, completeness of the journey, and fit to the target
   platform. Mobbin MCP results do not establish revenue, downloads, ratings,
   or business performance, so do not invent those signals or call a product a
   winner on metadata alone.
4. Record each product, canonical Mobbin URL, relevant screens or flows, and a
   short selection rationale in `research/<category>/references.md`.

## Phase 2 — Study the complete evidence

For each shortlisted product, inspect every image in the relevant returned
flow, in order. Page through `search_flows` while `has_next_page` remains true
and additional results still affect the specification. Use app-named
`search_screens` queries for pivotal surfaces not clear in the flow previews.

Read across products, not just within one:

- What does the first-use moment promise, and what action is primary?
- How long is onboarding, and what does each step earn: permission,
  personalization data, trust, or commitment?
- Where does monetization appear, and how are trial, price, value, and risk
  framed?
- What is the home-screen information hierarchy, and what sits one action away?
- How do empty, loading, error, offline, completion, and returning-user states
  behave?
- Which elements remain consistent as the user moves between screens?

Write the synthesis into `patterns.md`: conventions repeated across products,
choices where strong products diverge, notable edge cases, and recurring
weaknesses that create an opportunity. Every conclusion should point to one or
more Mobbin URLs.

## Phase 3 — Go frame by frame on the strongest three

Choose the three references most useful for the brief. Re-run precise,
app-named flow or screen searches where needed, using `exclude_screen_ids` to
avoid repeats in screen searches. For each decisive screen, state:

1. its single primary job;
2. how hierarchy, copy, controls, spacing, and motion support that job;
3. what should be adopted as a convention;
4. what should be changed for the user's product and why.

Inspect the images directly. Do not infer screen content from a flow name,
action label, or app name.

## Phase 4 — Turn research into a specification

Write the product specification from the evidence: the best-supported patterns
minus unnecessary complexity, plus the opportunity found in Phase 2. Include:

- screens and states in journey order;
- the job, information hierarchy, and primary action of each screen;
- component and copy conventions;
- accessibility and responsive behavior;
- the navigation map: push, modal, sheet, overlay, or root; what Back does; and
  one-way transitions such as completed onboarding, purchase, or submission;
- explicit Mobbin links supporting each important design decision.

Get user sign-off when they are actively collaborating. Otherwise, state the
material choices and proceed within the requested scope.

## Phase 5 — Build screen by screen

For every screen or section, in journey order:

1. Re-open the local references. Run a focused Mobbin search only when the
   existing evidence leaves a specific design question unanswered.
2. For mobile work, implement with `mobbin-app-design-skill` end to end. For
   web work, use `frontend-design`. Preserve the established design system,
   semantic colors, accessibility, state architecture, and motion language.
3. Create only the image assets the product genuinely needs, using one coherent
   visual system across the experience.
4. Run the product in its real preview environment. Capture the result, compare
   it side by side with the strongest Mobbin references, exercise interactions
   and transitions, fix the visible or behavioral gaps, and repeat.
5. Check small and large viewports or devices, light and dark themes where
   supported, safe areas, enlarged text, reduced motion, loading and error
   states, keyboard behavior, and platform-specific Back behavior.

## Phase 6 — Hold the bar

Walk the complete experience three ways:

- happy path;
- skeptical path, skipping everything optional;
- abuse path, including invalid input, offline or failed requests, interruptions,
  repeated actions, and every Back path.

Compare each decisive state with the best relevant reference. If the result is
weaker in hierarchy, clarity, feedback, accessibility, motion, or navigation,
put it back through the implementation and preview loop before declaring the
work finished.

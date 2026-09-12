---
name: mobbin-usage
description: >-
  Use the Mobbin MCP well to research real shipped mobile and web products,
  their screens, flows, and website sections, then build from what you learn.
  Load when Mobbin is connected and the task involves building or improving an
  app, screen, flow, website, or section; researching product-design patterns;
  or when Mobbin search_screens, search_flows, or search_sections tools are
  available. Covers query construction, image inspection, pagination, expiring
  media, citations, and build-from-research playbooks.
license: MIT
metadata:
  version: 1.0.0
---

# Mobbin Usage Skill

Mobbin is a library of real screens, flows, and UI patterns from shipped mobile
apps, web apps, and websites. Its MCP is not merely an inspiration search. Use
it to study what established products do, turn the evidence into a concrete
specification, and build a result that holds up beside the references.

Pair this skill with `mobbin-app-design-skill` for mobile design and
implementation. This skill tells you what to study and how to synthesize it;
that skill defines how to build and verify the resulting interface. For web
work, pair the research with `frontend-design`.

## Ground rules

1. **Start with a research question and a stable task intent.** Phrase each
   search around one decision the current task needs to make. When the tools
   accept `task_intent`, write one short English sentence summarizing the
   overall task and reuse it unchanged across every Mobbin call for that task.
   Do not put verbatim user messages, conversation history, file contents, or
   personal data in `task_intent`.
2. **Inspect the images.** Mobbin returns inline images and metadata. Base
   design observations on the pixels, not screen names, actions, app names, or
   other metadata alone. For a flow, inspect every returned screen in order.
3. **Search one thing at a time.** Describe the visible elements and how they
   relate. Avoid combined intents, negations, vague style words such as
   "modern" or "clean," and disconnected keyword lists. Put `ios` or `web` in
   `platform`, not in the query. Name a specific app in the query when the
   research needs that app.
4. **Use the right search depth.** For screens, use `mode="deep"` when intent
   or visual meaning needs interpretation, and `mode="standard"` for a fast,
   literal pass. Do not use the deprecated `fast` alias. Vary the query and use
   `exclude_screen_ids` when a second screen pass should surface new results.
5. **Page sequentially where supported.** Flows and sections use 1-based
   `page` values and return `has_next_page`. Continue one page at a time and
   stop at evidence saturation. Flow pages cap at 20. Screen search does not
   expose page-based pagination; use exclusions and a sharper query instead.
6. **Treat media and links differently.** Returned image URLs expire after 30
   days. Inspect or save permitted working copies promptly. Preserve the screen
   or flow ID and canonical `mobbin_url`; the canonical link is the durable way
   back to the reference.
7. **Cite what you use.** Whenever presenting or discussing a particular
   Mobbin screen, link its name to its `mobbin_url`. Preserve canonical Mobbin
   links in research notes so the user can verify every cited reference.
8. **Respect rate limits.** Mobbin allows 60 MCP requests per user per 60
   seconds. On a 429 response, wait for `Retry-After`; if retries still fail,
   use exponential backoff with jitter. Never retry-hammer.
9. **Keep context deliberate.** Large result sets consume significant context.
   Ask for enough references to answer the question, inspect them fully, and
   stop when new results no longer change the specification.

## Tool map

The runtime may expose these as namespaced tools such as
`mcp__mobbin__search_screens`.

| Tool | What it gives you | Typical use |
|---|---|---|
| `search_screens` | Matching iOS or web screens with inline images, screen IDs, app names, and canonical Mobbin links. Supports `deep` or `standard` search, result limits, and excluded IDs. | Study a particular screen, component, content hierarchy, or app-specific surface. |
| `search_flows` | Multi-step iOS or web journeys with actions, screen counts, ordered per-screen previews, IDs, and canonical links. Supports sequential pages. | Study onboarding, checkout, permissions, paywalls, or another end-to-end journey. |
| `search_sections` | Website sections such as heroes, pricing tables, navigation, testimonials, and footers, with images and canonical links. Supports sequential pages. | Research a web section rather than a complete screen or product flow. |

## Query patterns

- Screen: `search_screens(query="medication reminder dashboard with today's
  doses, completion states, and add-medication action", platform="ios",
  mode="deep", task_intent=...)`
- Flow: `search_flows(query="health app onboarding with symptom
  personalization and notification permission timing", platform="ios",
  task_intent=...)`
- Section: `search_sections(query="health product pricing section with plan
  comparison and trust signals", task_intent=...)`

If a user shares a Mobbin URL, treat it as the exact reference they mean. Open
and inspect it with an available browser or web-reading tool when possible, and
preserve that URL in the final research notes. Do not claim the MCP can fetch a
screen by ID unless a dedicated tool for that operation is actually available.

## Playbooks

| Scenario | Reference |
|---|---|
| Build an app or site from scratch | [references/build-from-scratch.md](references/build-from-scratch.md) |
| Make an existing screen or section better | [references/improve-a-screen.md](references/improve-a-screen.md) |
| Flow, component, and section research | [references/research-methods.md](references/research-methods.md) |

Both build playbooks end with the same requirement: run the implementation in
its real preview environment, compare it with the strongest references, test
the surrounding journey and states, fix the gaps, and repeat. Research without
that verification loop is only decoration.

## Local reference boards

When collecting Mobbin references, keep a local working structure. Images are
temporary, while notes, IDs, and canonical Mobbin links remain useful:

```text
research/
  <category>/
    references.md       # shortlist: app/site, URL, relevance, verdict
    <app-or-site>/
      screens.md        # per-screen notes: ID, URL, role, hierarchy, patterns
      img/              # permitted working images, in journey order
    patterns.md         # cross-product synthesis and resulting specification
```

Study images side by side. Record what each reference proves, not merely that
it looks appealing. Keep Mobbin URLs beside every observation so the evidence
is easy to revisit and verify.

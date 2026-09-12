# Image and illustration assets — generation pipeline

App-quality artwork needs a defined visual system, candidate selection, and
on-device verification. Do not ship the first generation without inspection.

## 1. Define the style system first

Record once per product:

- style family, such as flat duotone, paper collage, hand-drawn ink, 3D clay,
  restrained gradient, or photography;
- three to five palette colors from the actual design tokens, including the
  exact surface color behind the artwork;
- consistent lighting, material, and texture language;
- subject grammar: mascot, objects, people, abstract forms, or scenes;
- framing rules and reserved negative space for interface content.

Every asset prompt combines that system with a specific subject. Consistency
across the set matters more than maximizing novelty per asset.

## 2. Generate with the best available tool

- Use the largest useful generation size and highest appropriate quality, then
  downscale. Target at least twice the largest rendered pixel dimensions and
  never upscale a small generation.
- Generate several candidates, choose the strongest, and regenerate the rest of
  the set if the winner defines a better style direction.
- For repeated icons or objects, generate them together when that improves
  palette, lighting, and line-weight consistency.
- Request true transparency when supported, or the exact solid surface color.
  Inspect edges at high zoom for halos, matte fringes, and compression artifacts.
- Use an existing asset system when the product already has one; do not replace
  it with generated art merely because generation is available.

## 3. Prompt structure

```text
[subject], [style family], [palette names and hex values], [lighting and
material], [composition and reserved negative space], app illustration,
transparent or solid background [hex], no text, no watermark
```

- Exclude text unless the asset is intentionally typographic; generated labels
  are rarely production-ready.
- Keep empty-state scenes quiet and subordinate to the recovery action.
- Let celebration art imply motion through composition instead of literal speed
  lines everywhere.
- Reserve the area occupied by headlines and controls rather than hoping the
  layout can crop around the subject.

## 4. Post-process

1. Trim to content with a consistent padding rule.
2. Export the project's required density variants or a correctly sized source
   for the image pipeline. Use efficient modern formats for large photography
   when supported.
3. Verify artwork on device in every supported theme. Generate theme-specific
   twins or use a theme-invariant surface when one image cannot work on both.
4. Compress without visible damage. A decorative screen-level illustration
   should not impose multi-megabyte cost.
5. Add accessible descriptions only when the image communicates information;
   mark purely decorative art appropriately.

## 5. App icons and store assets

- Produce the master app icon at the platform-required size, without baked-in
  rounded corners. Follow platform transparency rules.
- Test the concept at small launcher sizes; simplify when the silhouette or
  focal idea disappears.
- Keep store screenshots and marketing artwork in the same visual family as the
  product while respecting their different communication role.

## 6. Quality gate

Reject and regenerate or repair an asset when:

- style, palette, lighting, or line weight drifts from the set;
- its edges show a halo, fringe, or obvious compression damage;
- it contains accidental text, signatures, or watermark artifacts;
- the composition collides with safe areas, headlines, or controls;
- it becomes illegible at its rendered size;
- it reads as unart-directed default model output rather than part of the brand.

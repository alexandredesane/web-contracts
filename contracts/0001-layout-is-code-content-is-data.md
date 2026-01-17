# 0001 — Layout is code, content is data

## Intent
Prevent CMS-driven rewrites and frontend degradation by clearly separating
**structure** from **editable content**.

This contract exists to protect frontend intent over time.

## Non-goals
- This is not about choosing a CMS
- This does not prescribe a specific framework
- This does not forbid dynamic content

## The contract
- **Layout stays in code**
  - Markup structure
  - Component composition
  - Spacing, hierarchy, interaction boundaries
- **Content becomes data**
  - Text
  - Media
  - Lists
  - Metadata

Editors can change data.
They cannot change structure.

## Rationale
Frontend structure already exists:
- components define contracts
- props define configurability
- pages define composition

Rebuilding layout inside a CMS duplicates responsibility and introduces drift.

## Examples

### Good

``
<Hero
  title={content.title}
  subtitle={content.subtitle}
  image={content.image}
/>
``

The component owns layout.<br>
The CMS only provides values.

### Bad

- Page builders
- Drag-and-drop block editors
- CMS-managed templates reimplementing frontend structure

These systems allow content tools to rewrite design intent.

## Failure modes

- Adding “just one layout option” in the CMS
- Letting editors reorder structural blocks
- Treating CMS templates as the source of truth

These always scale into full rewrites.

## Escape hatches

- Prototyping
- Marketing-driven landing pages
- One-off experiments

When breaking this contract, document it explicitly.

## Related contracts

- [0002 — State ownership](./contracts/0002-state-ownership.md)
- 0003 — Build-time first
- 0007 — No implicit coupling
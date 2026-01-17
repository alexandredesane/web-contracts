# 0002 — State ownership

## Intent
Avoid hidden coupling and unpredictable behavior by making **state ownership explicit**.

Every piece of state must have a single, clear owner.

## Non-goals
- This is not about banning shared state
- This does not require global state managers
- This does not forbid interactivity

## The contract
- Every state has **one owner**
- Other systems may **observe**, not mutate
- Ownership is explicit and documented

If ownership is unclear, the architecture is already broken.

## Rationale

Most frontend bugs are not rendering bugs.
They are **state coordination bugs**.

Implicit state ownership leads to:
- race conditions
- double updates
- “who changed this?” debugging

## Examples

### Good

`<x-dialog :open="open" @x-close="open = false"></x-dialog>`

The dialog owns its open/close behavior.<br>
Alpine owns the state.<br>
The dialog reacts to it.

Ownership is clear.

### Bad

- Multiple components mutating the same DOM state
- Components reaching into each other to toggle flags
- Implicit state via DOM queries or IDs

These patterns scale poorly.

## Failure modes

- “Temporary” shared state
- Bidirectional data flow without contracts
- Hidden mutations via side effects

These always resurface later as bugs.

## Escape hatches

- Transitional refactors
- Legacy systems
- Debug tooling

If state ownership is shared, document why and for how long.

## Related contracts

- [0001 — Layout is code, content is data](./contracts/0001-layout-is-code-content-is-data.md)
- 0006 — Events, not callbacks
- 0007 — No implicit coupling
# ADR-001: Semantic design tokens over raw hex values

**Status:** Accepted  
**Date:** 2024-01-01

## Context

Applications could reference colours directly (`#1E1E1E`), but this creates
tight coupling to specific theme values and makes theme switching require
app-level code changes.

## Decision

`ColorPalette` maps semantic names (`"background"`, `"accent"`) to `Color`
values. Applications reference tokens by name; the engine swaps palettes at
runtime.

## Consequences

- Swapping the active theme requires only a palette reload — apps need no changes.
- Token names form a public API; renaming them is a breaking change.
- Apps that need a colour not in the palette must add a new token name (requires
  coordination).

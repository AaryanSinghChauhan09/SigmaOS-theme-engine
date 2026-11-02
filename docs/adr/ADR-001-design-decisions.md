# ADR-001: Theme Engine Design Decisions

**Date:** 2024-01-01  
**Status:** Accepted  
**Component:** SigmaOS-theme-engine

---

## Context

SigmaOS needs a theme system that supports dark/light switching, icon theming, and real-time reload without restarting apps.

## Decisions

### 1. Semantic design tokens, not hardcoded colors

**Rationale:** Tokens (`background`, `foreground`, `accent`) decouple the visual identity from widget code. Switching themes is a single palette swap.

### 2. CSS variable rendering for GTK4

**Rationale:** GTK4's CSS provider supports custom properties. Mapping tokens to `--sigma-*` variables lets all widgets respond to theme changes by updating one CSS provider.

### 3. XDG icon theme inheritance chain

**Rationale:** The XDG spec is the Linux desktop standard. Following it means SigmaOS is compatible with existing icon packs (Papirus, Adwaita, etc.) out of the box.

### 4. Palette generation from a single accent color

**Rationale:** Material Design 3's tonal palette model produces harmonious color scales from one seed color. This powers per-user accent customization.

### 5. WCAG contrast check as first-class API

**Rationale:** Accessibility is a requirement, not an afterthought. The `meets_wcag_aa` function lets the theme engine refuse color combinations that fail AA contrast.

## Consequences

- Theme changes are zero-restart: GTK4 CSS provider is updated in place.
- Icon theme registry is separate from color palette — they can be changed independently.
- Contrast validation runs at theme-build time, not at render time.

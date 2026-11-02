# Extraction Log — SigmaOS-theme-engine

## Source
Extracted from: `SigmaOS-desktop` monorepo, `shell/theme/` subtree.

## What Was Extracted

| Module | Source path | Notes |
|--------|------------|-------|
| css.rs | shell/theme/css.rs | CSS variable rendering extracted cleanly |
| icons.rs | shell/theme/icons.rs | XDG icon lookup; cache deferred |
| palette.rs | shell/theme/palette.rs | Tonal scale + WCAG contrast helpers |
| lib.rs core | shell/theme/engine.rs | ThemeEngine, ColorPalette, ThemeRenderer |

## Decisions Made During Extraction

1. **Removed GTK CSS provider calls from lib** — GTK4 provider setup belongs in the app binary, not the library. The library returns CSS strings/maps.
2. **WCAG helpers promoted to public API** — previously internal; now first-class for use by settings accessibility panel.
3. **Icon cache deferred** — thumbnail/icon caching will use `SigmaOS-file-manager`'s ThumbnailCache pattern.

## Known TODOs

- [ ] inotify-based hot reload watcher
- [ ] GTK4 CSS provider wrapper (in app framework)
- [ ] SVG icon rendering at arbitrary sizes
- [ ] Per-user theme persistence via XDG config

## Date
2024-01-01

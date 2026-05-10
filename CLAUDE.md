# Noogat Site — Claude Code Guide

This is the marketing/legal site for the Noogat iOS app, hosted at `https://mcfredrick.github.io/noogat-site/`.

## Design System

**For all aesthetic decisions** — colors, fonts, gradients, logo usage — refer to the canonical design system:

```
/Users/matt/Code/claude-inbox/DESIGN_SYSTEM.md
```

That file is the single source of truth for brand colors, typography, theming rules, and logo asset locations. The CSS variables in `_shared.css` and `landing-page.html` must stay in sync with it.

## File Map

| File | Purpose |
|---|---|
| `landing-page.html` | Main marketing landing page (self-contained styles) |
| `_shared.css` | Shared styles for privacy + terms pages |
| `privacy/index.html` | Privacy policy |
| `terms/index.html` | Terms of service |
| `assets/` | Logo images (transparent, white BG, black BG variants) |

## Deployment

Static site served directly from GitHub Pages. Push to `main` to deploy — no build step.

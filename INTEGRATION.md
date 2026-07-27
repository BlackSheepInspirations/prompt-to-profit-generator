# Prompt to Profit — Black Sheep integration notes

How Prompt to Profit (a.k.a. **Prompt Haus**) connects to the rest of the Black
Sheep Hausen. Verified against the live Hausen codebase (2026-07). Keep this in
sync; the other pieces live in `/Users/blacksheepcreations/AI Creators Prompt Haus`.

## Brand DNA bridge — copy/paste (works anywhere, already built)

P2P's **"Import your Brand DNA"** panel parses this block (case-insensitive;
accepts `tone`/`voice`, `visual`/`aesthetic`):

```
BLACK SHEEP BRAND DNA
Mode: Product            # or "Brand" / "Creator" / "Niche"
Brand tone: Warm, Friendly, Calm
Visual style: Organic, Minimal
Colors: #C97C5D, #8B5E3C, #F5F0E6
Keywords: community, belonging, handmade
Avoid: cheap, generic, salesy
```

Brand Haus should expose a **"Copy for Prompt to Profit"** button that emits
exactly this. Maps to: `brandTone`, `visualStyle` (fuzzy multi-match + custom
field), `colorDirection = brand-colors`, `wordsToInclude`, `wordsToAvoid`, and
the brand-mode toggle.

## Brand Kit auto-port — shared vault (to build once co-located)

Do **not** invent a new channel. Brand Haus is the authoritative source and
mirrors its kits into a shared, read-only key on every save:

- Key: `localStorage["blackSheepBrandKitVault"]`
- Shape:
  ```json
  { "brandHausKits": [
    { "id": "...", "source": "brandHaus", "name": "...", "savedAt": "...",
      "colors": ["#hex", "..."], "headingFont": "str", "bodyFont": "str",
      "mood": "str", "voice": "str", "coreValues": ["..."], "mission": "str" }
  ]}
  ```
- Marketing / Graphics / Product Haus **read** this key read-only. **P2P must do
  the same — read only, never write** (keeps it live, not a stale copy).
- P2P's own private kits (if added) go under `promptHausBrandKits`. Content Haus
  does not participate in sharing.

**P2P mapping for auto-port:** `voice → brandTone`, `mood → visualStyle`,
`coreValues → wordsToInclude`, `colors → colorDirection = brand-colors`.
`headingFont`/`bodyFont`/`mission` have no P2P field yet (skip or note).

## Shopify embed pattern (for migrating P2P into the suite)

Each Haus is a **native Shopify section** (`sections/<haus>.liquid`), not an
iframe:

- Renders a mount point: `<div id="<haus>-app"></div>` (P2P → `prompt-haus-app`).
- Gated by `customer.tags contains section.settings.access_tag`, with a
  `request.design_mode` bypass so it shows in the theme editor.
- Loads a **vanilla-JS, no-build** app via `<script src="{{ 'file.js' | asset_url }}" defer>`.
- The Hausen re-render the whole panel (`root.innerHTML = ""`) on every state
  change. P2P currently uses static HTML + incremental updates; migrating means
  wrapping its markup in the section + `asset_url` paths + the tag gate. It does
  **not** have to adopt the full re-render pattern to coexist.

## Shared palette (the real one — for aligning P2P to the suite)

Base (shared across Hausen):
- Cream `#F2F0EB` (Content Haus uses `#FAF6EF`)
- Black `#1A1815`
- Gold `#C9A84C`
- Teal `#0D7377`
- Charcoal `#2E2A26`

Per-Haus accent (var is confusingly named `--<x>-espresso` everywhere):
- Brand Haus — teal `#0D7377`
- Content Haus — brown `#3C2A21`
- Product Haus — blue `#2563EB`
- Graphics Haus — purple `#5B3C8C`
- Marketing Haus — pink `#D6336C`
- Prompt to Profit — (unassigned; proposal: a profit green)

> Note: Marketing Haus's `--mh-gold` is actually `#6B6860` (grayish) — a known
> mislabeled leftover, not real gold.

Fonts: no locked pairing. Lora + Open Sans are options in the Branding Studio's
font list (5 web-safe + 14 Google), but the real pairing is whatever a saved
Brand Kit sets. Don't treat Lora/Open Sans as a fixed standard.

## P2P's own current look (needs alignment if it joins the suite)

P2P currently ships teal `#0b5e59`/`#0aa89b` + gold `#e6b955` — close but **not**
the shared values. Because P2P is 100% CSS-token-driven, aligning it to the
shared palette (`#0D7377` teal, `#C9A84C` gold, `#F2F0EB` cream, `#1A1815` black)
is a quick token swap.

# Palette Designer

A single-file, offline-first tool for turning two brand colours into a complete, accessible light + dark colour system — with WCAG readability checked automatically on every token.

No build step, no dependencies, no server. Open `palette-forge.html` in a browser and it works.

---

## Why

Picking a primary and secondary colour is the easy part. Turning them into a full set of tokens — backgrounds, surfaces, borders, muted text, hover states, semantic colours — that stay readable in both light and dark mode is the part that usually gets guessed at. Palette Forge does that derivation for you and shows the maths behind every decision, so you can trust the output instead of eyeballing it.

## Features

- **Two-colour input** — pick a primary and secondary via colour picker or hex field, with live validation.
- **Randomiser** — generates harmonious pairs (complementary, analogous, triadic, split-complementary, monochromatic, or "surprise me"). Press <kbd>R</kbd> anywhere on the page.
- **10 built-in presets** — Ocean Depths, Sunset Boulevard, Forest Canopy, Modern Minimalist, Golden Hour, Arctic Frost, Desert Rose, Tech Innovation, Botanical Garden, Midnight Galaxy.
- **Full light + dark scheme generation** — background, surface, surface-alt, border, text, muted text, primary/secondary (plus hover and "on-colour" label variants), tinted subtle fills, and success/warning/error states. Every text-bearing token is automatically nudged until it clears its WCAG target — nothing here is a guess.
- **Readability grade on every colour** — AAA / AA / AA-Large / Fail badges with the exact contrast ratio, measured against the colour each token actually sits on.
- **Contrast matrix** — every text colour × every background, cross-referenced in one table.
- **Tonal scales** — 50→950 ramps for both colours, for hover states, charts, and borders.
- **Four live previews** — the same tokens rendered as a dashboard app, a marketing landing page, a data table, and a mobile app screen, so you can see how the palette behaves across real interface patterns, not just swatches.
- **Export in four formats** — CSS custom properties, SCSS variables, a Tailwind config excerpt, and JSON design tokens (with contrast ratios baked in).
- **Built-in WCAG explainer** — a plain-language rundown of what contrast ratio, AA, AAA, and large-text thresholds actually mean, for anyone on the team who isn't already fluent in accessibility jargon.
- **Mobile friendly** — fully responsive down to small phone widths; touch-sized controls, horizontally scrollable ramps/tables where content is naturally dense, and a collapsed layout for the tightest screens.
- **Copy anything** — click any swatch, hex value, or ramp step to copy it straight to your clipboard.

## Getting started

Palette Designer is one HTML file with inline CSS and JavaScript. There's nothing to install.

```bash
# clone or download, then just open it
open palette.html      # macOS
xdg-open palette.html  # Linux
start palette.html     # Windows
```

Or host it anywhere that serves static files — GitHub Pages, Netlify, a plain S3 bucket, or your own server. It has no external dependencies and makes no network requests.

### GitHub Pages

1. Push this repo to GitHub.
2. Settings → Pages → Deploy from branch → select `main` (or your default branch) and `/ (root)`.
3. Your tool is live at `https://adelando.github.io/pallet-designer/palette.html`.

## How it works

1. **You define primary + secondary** — either directly, via a preset, or via the randomiser.
2. **Backgrounds and surfaces are derived** from the primary's hue at very low saturation, so the whole UI feels tied to the brand colour without being loud about it.
3. **Text colours are generated, then verified** — Palette Forge doesn't just pick a colour and hope; it walks the lightness of each text token up or down in small steps until it actually clears its WCAG target against the background it will sit on (7:1 for body text, 4.5:1 for muted text and links, 3:1 for solid UI fills like buttons).
4. **Dark mode isn't an inverted light mode** — accent colours are independently lightened and desaturated for dark surfaces (following the same logic design systems like Material Design use), because a saturated light-mode primary usually vibrates uncomfortably on a dark background if used as-is.
5. **Semantic colours** (success / warning / error) borrow their saturation character from your brand colours so they don't look like they were airlifted in from a different app, while keeping their conventional green/amber/red hues for recognisability.

## Understanding the readability grades

Palette Designer checks contrast per the [WCAG](https://www.w3.org/WAI/WCAG21/quickref/) (Web Content Accessibility Guidelines) 2.x relative-luminance formula — the same maths behind most accessibility linters and legal accessibility requirements.

| Badge | Ratio | Meaning |
|---|---|---|
| **AAA** | ≥ 7.0:1 | Enhanced level. Comfortable for body text; harder to hit with saturated brand colours. |
| **AA** | ≥ 4.5:1 | The practical floor most products and accessibility laws reference. Target for body text and links. |
| **AA · Large** | ≥ 3.0:1 | Relaxed minimum for large text (≈18pt/24px regular or 14pt/18.5px bold) and non-text UI elements like button outlines and icons. |
| **Fail** | < 3.0:1 | Genuine accessibility failure — illegible for a meaningful share of readers. |

The app itself has a collapsible "What is WCAG?" panel at the top with a longer explanation, if you want to read more or share context with teammates who are new to this.

**A note on APCA:** this tool measures WCAG 2.x contrast, which remains the ratified standard most tooling and regulation is built on. APCA (used in the draft WCAG 3) is a newer perceptual contrast model that some designers prefer, particularly for light text on dark backgrounds — worth knowing if a ratio here ever feels stricter or looser than a colour looks in practice.

## Export formats

Copy tokens straight into your codebase:

- **CSS variables** — `:root { --color-primary: ... }` with a `prefers-color-scheme: dark` block and a `.dark` class variant.
- **SCSS** — `$light-*` / `$dark-*` variables plus Sass maps for the tonal scales.
- **Tailwind config** — a `theme.extend.colors` object ready to paste into `tailwind.config.js`.
- **JSON tokens** — every token with its hex value, contrast ratio against its surface, and WCAG grade, for design-token pipelines (Style Dictionary, Tokens Studio, etc.).

## Browser support

Works in any current version of Chrome, Firefox, Safari, or Edge. Uses CSS custom properties, `clamp()`, `aspect-ratio`, and `backdrop-filter`; the latter degrades gracefully (solid header instead of blur) on anything that doesn't support it.

## Credits

Preset palettes are drawn from a curated reference-theme collection (Ocean Depths, Sunset Boulevard, Forest Canopy, and the rest) originally assembled for presentation styling, repurposed here as colour-scheme starting points.

## License

MIT — do whatever you like with it. Attribution appreciated but not required.

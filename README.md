# FuseRemit

Astro 5 + Tailwind CSS 4 static site. Two full-screen sections — the hero and a
three-step "How it works" band — plus a footer, built to match the supplied
design renders.

## Commands

```bash
npm install
npm run dev      # http://localhost:4321
npm run build    # static output in dist/
npm run preview  # serve dist/
npm run check    # astro + TypeScript diagnostics
```

## Structure

```
public/images/
  fuseremit-logo.webp   trimmed wordmark (713x160, transparent)
  fuseremit-mark.png    F mark only, used as the favicon
  hero-scene.webp       transparent 3D phone + globe scene
  steps/coins.webp      step 1 illustration
  steps/person.webp     step 2 illustration
  steps/plane.webp      step 3 illustration
src/
  components/Navbar.astro        logo + links + Get started, with a mobile menu
  components/Hero.astro          copy, CTAs, 3D scene
  components/StepsSection.astro  heading, three glass step cards, connectors
  components/Footer.astro        brand, link columns, legal bar
  components/VideoModal.astro    "See how it works" dialog
  layouts/Layout.astro           html shell, meta, Poppins
  pages/index.astro              page wrapper carrying the shared background
  styles/global.css              theme tokens, .page-wash, .glass, .step-body
```

## How the layout works

**One background, no seams.** `.page-wash` on the page wrapper paints a single
vertical gradient behind the hero, the steps section and the footer. Each
section adds only *translucent* accent layers on top, and those layers are
masked to fade at the join, so there is no hard line between sections.

**Everything fits the viewport.** Both sections are `min-h-svh`. Inside the
steps section every vertical metric derives from `--band` (the illustration
height) and `vh` units, so type, padding, card overlap and the badge all scale
together instead of overflowing on a shorter screen.

**Equal-height cards.** The step cards are flex children with `flex-1`, so
their bottoms stay level even when one body wraps to an extra line.

## Design tokens

Sampled pixel-for-pixel from the reference renders, defined in
`src/styles/global.css`:

| Token | Value | Used for |
| --- | --- | --- |
| `--color-ink` | `#061043` | headlines, card titles |
| `--color-ink-soft` | `#131C53` | nav links |
| `--color-brand` | `#0360FC` | "Share a moment.", eyebrow, step numbers |
| `--color-brand-bright` → `--color-brand-deep` | `#0B66F3` → `#0143BC` | button gradient (`.btn-brand`) |
| `--color-brand-ink` | `#0B35D0` | "Explore how it works" |
| `--color-brand-ring` | `#2E51D6` | hero eyebrow pill text |
| `--color-muted` | `#6B7AAF` | hero sub-headline |
| `--color-slate` | `#525E85` | steps sub-headline, card and footer copy |
| `--color-pill` | `#E5EFFE` | eyebrow pill background |
| `--color-hairline` | `#D7E5F8` | outline button / borders |

## Notes

- The 3D scenes are the supplied renders, trimmed to their alpha bounds and
  converted to WebP — an exact match rather than a CSS re-creation. This cut
  the image payload from ~4.5 MB to ~510 KB.
- Poppins runs wider than the face used in the reference renders, so the step
  body copy is set a little smaller to keep the reference's two-line wrap. For
  the same reason `.step-body` only applies the reference's title-aligned
  indent at `2xl` and up, where there is room for it.
- `VideoModal.astro` is a native `<dialog>`; drop an `<iframe>` or `<video>`
  into the `aspect-video` block to wire up a real walkthrough.
- Motion respects `prefers-reduced-motion`.
- Footer and nav links are placeholders (`#`) — no pages exist behind them yet.

# FuseRemit — hero

Astro 5 + Tailwind CSS 4 static site. The landing hero is a pixel match of the
`Blue fintech money transfer hero` reference: navbar, copy block and the 3D
money-transfer scene.

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
  fuseremit-logo.png   trimmed wordmark (1806x405, transparent)
  fuseremit-mark.png   F mark only, used as the favicon
  hero-scene.png       transparent 3D phone + globe scene
  hero-bg.png          original wide hero render, kept as a reference/alternative
src/
  components/Navbar.astro      logo + links + Get started, with a mobile menu
  components/Hero.astro        background, copy, CTAs, 3D scene
  components/VideoModal.astro  "See how it works" dialog
  layouts/Layout.astro         html shell, meta, Poppins
  pages/index.astro
  styles/global.css            theme tokens + button gradient
```

## Design tokens

Sampled pixel-for-pixel from the reference render and defined in
`src/styles/global.css`:

| Token | Value | Used for |
| --- | --- | --- |
| `--color-ink` | `#061043` | "Send money." |
| `--color-ink-soft` | `#131C53` | nav links |
| `--color-brand` | `#0360FC` | "Share a moment." |
| `--color-brand-bright` → `--color-brand-deep` | `#0B66F3` → `#0143BC` | button gradient (`.btn-brand`) |
| `--color-brand-ring` | `#2E51D6` | eyebrow pill text |
| `--color-muted` | `#6B7AAF` | sub-headline |
| `--color-pill` | `#E5EFFE` | eyebrow pill background |
| `--color-hairline` | `#D7E5F8` | outline button / borders |

Hero background is a `112deg` gradient (`#FBFDFE → #F6FAFE → #ECF5FD → #E3EFFC`)
with three radial glows, matching the reference's left-to-right cool shift.

## Notes

- The 3D scene is the supplied transparent PNG, so it is an exact match rather
  than a CSS re-creation. The phone card could be rebuilt as live HTML later if
  the numbers need to be dynamic.
- `VideoModal.astro` is a native `<dialog>`; drop an `<iframe>` or `<video>` into
  the `aspect-video` block to wire up a real walkthrough.
- Motion respects `prefers-reduced-motion`.

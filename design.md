# ApnaAstro Landing — Design System

A design spec for the ApnaAstro marketing landing page, adapted from the clean,
minimal, conversion-focused aesthetic of **pop.site** (a micro-site builder).
ApnaAstro is a **white-label astrology SaaS** — the page sells the *platform* to
astrology businesses, so the tone is "launch your own stunning astrology app,
easily." Keep it clean, spacious, confident — not mystical/cluttered.

> Source of inspiration: https://pop.site/ — "Make a stunning site, easily",
> whitespace-heavy, pill CTAs, modular feature cards, heavy social proof.

---

## 1. Brand & mood

- **Three words:** Clean · Confident · Effortless.
- **Feel:** modern SaaS (Stripe/Linear/pop.site lineage) with a warm cosmic
  accent — NOT heavy purple-galaxy clichés. White canvas, one strong accent,
  generous whitespace, big type.
- **Do:** lots of air, one accent colour, rounded cards, soft shadows, a single
  clear CTA repeated down the page ("Start free trial").
- **Don't:** dark mystical backgrounds, star-field noise, more than 2 brand
  colours, dense text.

## 2. Color palette

Light-first (pop.site is pure white). One warm accent + one gold secondary
(nods to astrology without going literal).

| Token | Hex | Use |
|-------|-----|-----|
| `--bg` | `#FFFFFF` | page background |
| `--bg-soft` | `#F7F6FB` | alternating section bands, cards |
| `--ink` | `#12101F` | headings, primary text |
| `--muted` | `#6B6880` | body / secondary text |
| `--line` | `#ECE9F5` | borders, dividers |
| `--primary` | `#7C4DFF` | CTAs, links, accent (cosmic violet) |
| `--primary-ink` | `#FFFFFF` | text on primary |
| `--accent` | `#FFB300` | secondary highlights, stars, badges (gold) |
| `--grad` | `linear-gradient(90deg,#7C4DFF,#FFB300)` | headline highlight, hero art |

**Dark mode (optional):** `--bg #0D0B16`, `--bg-soft #161327`, `--ink #F3F1FB`,
`--muted #A7A3BD`, `--line #241F3A` (accent/primary unchanged). Support via
`prefers-color-scheme`.

## 3. Typography

pop.site uses a clean geometric sans. Use a free web-safe stack (self-host or
system — the landing must stay dependency-free / CSP-safe, so prefer a system
stack unless bundling a font file into `assets/`).

- **Display / headings:** `"Plus Jakarta Sans", "Inter", -apple-system, sans-serif`,
  weight 800, tight tracking (`letter-spacing: -0.03em`).
- **Body:** same family, weight 400–500, `line-height: 1.6`, `color: var(--muted)`.
- **Scale:** hero H1 `clamp(2.2rem, 5vw, 3.6rem)`; section H2 `clamp(1.6rem, 3.5vw, 2.2rem)`;
  body `1.05–1.2rem`; captions `0.85rem`.
- **Highlight word** in the hero uses `--grad` via `background-clip: text`.

## 4. Layout & sections (top → bottom)

Mirror pop.site's flow, retargeted to selling the platform:

1. **Nav** — left wordmark (logo + "ApnaAstro"), right links (Features, How it
   works, Pricing) + a pill CTA "Book a demo". Sticky, transparent → solid on scroll.
2. **Hero** — pill eyebrow ("✨ White-label astrology platform"), big H1 with one
   gradient word ("Launch **your own** astrology app — your brand, not ours."),
   one-line sub, two CTAs (primary "Start free trial", ghost "See how it works"),
   a trust line ("Powering astrology businesses across India"). Optional hero art:
   a phone mock or a soft gradient blob — keep it light.
3. **Logos / social proof strip** — "Trusted by" or "Featured on" row (grey logos).
4. **Feature grid** — 6 rounded cards (icon + title + one line): Branded user &
   astrologer apps · Own admin panel · Isolated data · Landing page included ·
   Chat/call/live · Own payments & keys. This is the pop.site "sections showcase".
5. **How it works** — 4 numbered steps (Create tenant → Build apps → Go live →
   Manage & bill), each a soft card.
6. **Testimonial(s)** — 1–3 quotes with name/role (pop.site leans hard on these).
7. **Pricing / trial CTA band** — gradient-tinted panel: "Start with a 14-day free
   trial", one CTA. "No credit card to start."
8. **Footer** — wordmark, link columns (Product / Company / Legal), contact
   (hello@devifai.in), "© ApnaAstro · a DevifAI product".

## 5. Components

- **Buttons:** fully-rounded **pill** (`border-radius: 999px`), `padding: 14px 28px`,
  weight 700. Primary = solid `--primary` / white text; ghost = transparent with
  `1px solid --line`. Subtle hover lift (`translateY(-1px)` + shadow).
- **Cards:** `--bg-soft` fill, `1px solid --line`, `border-radius: 16px`,
  `padding: 24px`, soft shadow (`0 6px 24px -12px rgba(0,0,0,.15)`). Icon at top
  (emoji or simple line icon), title 1.1rem/700, body muted.
- **Pill eyebrow / badges:** small rounded chip, `--bg-soft` bg, `--muted` text,
  `0.8rem`, used above headings and for "New" tags.
- **Step number:** 34px circle, `--grad` fill, white bold numeral.
- **Section rhythm:** alternate `--bg` and `--bg-soft` bands; `padding: 52–72px 0`;
  content `max-width: 1040px`, centered.

## 6. Imagery & motion

- pop.site uses clean product screenshots + minimal graphics. For ApnaAstro:
  use **1 hero device mock** (a branded app screen) + **emoji or simple line
  icons** in feature cards. Avoid stock mystical photos.
- Motion: subtle only — fade/rise on scroll (IntersectionObserver), button hover
  lift. No autoplay galaxies. Keep the page **self-contained** (no external JS/CDN)
  to satisfy the static-host + CSP constraints (see below).

## 7. Constraints (important)

- The landing ships as a **single self-contained `index.html`** (static on Vercel).
  Inline all CSS; avoid external fonts/scripts/images where possible (CSP-safe,
  fast, no dependency). If a custom font or hero image is needed, put the file in
  `assets/` and reference it locally (bundle it, don't hotlink).
- Must be **responsive** (mobile-first; hero + grid collapse to one column) and
  **theme-aware** (light default, optional dark via `prefers-color-scheme`).
- Keep it accessible: real headings, sufficient contrast (violet `#7C4DFF` on white
  passes AA for large text; use `--ink` for body).

## 8. Assets

Put brand assets here in `assets/`:
- `logo.svg` — the ApnaAstro wordmark/mark (starter provided).
- `favicon.svg` / icon — derive from the mark.
- (optional) `hero.svg` / `hero.png` — hero device mock or gradient art.
- (optional) a self-hosted `.woff2` if not using the system font stack.

Current `index.html` already implements a first cut of sections 1–7 with the
palette above — treat this doc as the spec to refine it toward the pop.site polish.

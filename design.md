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

Mirror pop.site's flow, retargeted to selling the platform. **Every CTA opens the
contact modal** (see §5b) — direct-click psychology: one obvious next action
everywhere, low friction, phone capture.

1. **Nav** — left wordmark, right links (Features, Demos, How it works, Pricing),
   theme toggle + a pill CTA "Book a demo". Sticky, transparent → solid on scroll.
2. **Hero** — pill eyebrow ("✨ White-label astrology platform · Live in days"),
   big H1 with one gradient word ("Launch **your own** astrology app — your brand,
   not ours."), one-line sub, primary CTA "Start 14-day free trial →" + ghost
   "Watch demo", trust line (stars · "Free for 14 days · No credit card"). Hero art:
   **3 phone mockups** (Admin / User / Astrologer) fanned with rotation + soft
   shadow over a subtle gradient blob (see §6b).
3. **Logos / "everything on one platform" strip** — grey chip row.
4. **Demos** — 3 platform demo cards (see §6c): **User app** (phone frame),
   **Astrologer app** (phone frame), **Admin panel** (web 16:10 frame). Each has a
   video slot + play button (opens modal until real videos are dropped in). Section
   CTA: "Get all three — free for 14 days →".
5. **Feature grid** — 6 rounded cards (icon-in-tile + title + one line).
6. **How it works** — 4 numbered steps (Create tenant → Build apps → Go live →
   Manage & bill).
7. **Pricing** — 3 plan cards (see §5c) + "Most popular" highlight on the middle.
8. **Testimonials** — 3 quotes with avatar/name/role + 5 stars.
9. **Trial CTA band** — gradient-tinted panel, one CTA, "No credit card".
10. **Footer** — wordmark, link columns (Product / Company / Legal), contact.
11. **Sticky mobile CTA** — fixed bottom bar on mobile ("Start 14-day free trial →"),
    hides when the footer or modal is in view.

## 5b. Contact modal (all CTAs → this)

- Every button carries `data-open="<intent>"` (e.g. "Start free trial",
  "Monthly plan — ₹5,999/mo", "One-time buyout", "Demo — User app"). Clicking any
  opens a centered modal sheet; the intent is shown as a small chip + stored in a
  hidden field so we know which offer/plan the lead clicked.
- **Fields:** Name (required), **Phone** (required — `+91` country-code box +
  10-digit tel input, numeric), Email (optional). Submit = "Request my free trial →".
- Validates name + 10-digit phone client-side. On submit shows a success state
  ("You're on the list! 🎉" + WhatsApp number). Currently captures to
  `localStorage` (`aa-leads`) — **TODO: POST to a backend lead endpoint** when one
  exists. Esc / backdrop / ✕ closes; body scroll locks while open.

## 5c. Plans (monthly SaaS)

Three cards, middle = "Most popular":

| Plan | Price | Note |
|------|-------|------|
| **Free trial** | ₹0 for 14 days | Full access, no credit card |
| **Monthly** ⭐ | **₹5,999/month** per client | Everything, cancel anytime |
| **One-time** | One-time buyout (custom) | Own the platform outright |

All three CTAs open the contact modal (no public checkout).

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

- Motion: subtle only — fade/rise on scroll (IntersectionObserver), button hover
  lift. No autoplay galaxies. Page stays **self-contained** (no external JS/CDN).

## 6b. Hero phone mockups (pure CSS device frames)

Three `.phone` frames — `.left` (Admin), `.center` (User, front), `.right`
(Astrologer) — fanned:
- Frame: `width:236px`, dark gradient body, `border-radius:38px`, `padding:11px`,
  soft `--shadow`, a speaker pill via `::after`. Inner `.screen` = `border-radius:28px`,
  `overflow:hidden`, `aspect-ratio:9/19.3`.
- Side phones: `.left` `rotate(-6deg) translate scale(.9)`, `.right` `rotate(6deg)`;
  center on top (`z-index:3`). On ≤720px, side phones hide, center goes full.
- **Screenshot slot:** each `.screen` currently renders a branded placeholder
  (`.ph-fill` gradient + skeleton cards + caption). **To add real screenshots**,
  replace the placeholder with `<img src="assets/shot-user.png">` (object-fit:cover)
  inside `.screen`. Center=violet, left=dark, right=gold to hint the 3 surfaces.

## 6c. Demo video slots (3 platforms)

`#demos` = 3 `.demo` cards: two `.phoneframe` (9:16) for the mobile apps + one
16:10 for the web admin. Each `.frame` has a badge, a circular play button
(`data-open` → modal for now), and a "Demo video coming soon" hint.
- **To add a real demo video:** drop the file in `assets/` and replace the frame
  body with `<video src="assets/demo-user.mp4" poster="assets/poster-user.jpg"
  controls playsinline></video>` (bundle the file — no hotlinking, CSP-safe).
  Filenames expected: `demo-user.mp4`, `demo-astrologer.mp4`, `demo-admin.mp4`
  (+ optional `poster-*.jpg`).

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

Put brand + media assets here in `assets/`:
- `logo.svg` — the ApnaAstro wordmark/mark (provided).
- `favicon.svg` — derive from the mark (provided).
- **Screenshots (drop in later, wire per §6b):** `shot-user.png`,
  `shot-astrologer.png`, `shot-admin.png` (9:19.3 for phones; wide for admin).
- **Demo videos (drop in later, wire per §6c):** `demo-user.mp4`,
  `demo-astrologer.mp4`, `demo-admin.mp4` (+ optional `poster-*.jpg`). Bundle the
  files locally — do NOT hotlink (CSP + static-host constraint).

`index.html` implements ALL sections above (hero phone mockups, 3-platform demo
slots, 6 feature cards, 4 steps, 3 monthly plans, testimonials, trial band, sticky
mobile CTA, and a contact-form modal that every CTA opens). It is fully
self-contained, theme-aware (light/dark + a manual toggle), and responsive.
Screenshots/videos are the only things left to drop in — the slots are marked with
HTML comments in `index.html`.

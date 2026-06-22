# Shaade.design — Styleguide

Locked decisions. When in doubt, follow this. If a page deviates, fix the page.

---

## Palette

```css
/* Earth / Spanish villa palette */
--c-terracotta:  #DC8055;  /* warm orange (small accents, hover-pop) */
--c-rust:        #B05A30;  /* burnt rust — H1 italic emphasis, card arrows */
--c-clay:        #C18E78;  /* dusty rose — unused, available */
--c-brick:       #823526;  /* deep red — section eyebrows, arrow-hover */
--c-navy:        #11243F;  /* deep blue — strong CTAs, active states */
--c-deep-blue:   #1F4068;  /* mid-deep blue — testimonial italics, pull-quotes */
--c-steel:       #3A6991;  /* muted blue — card-tag hover, avatar TM */
--c-gold:        #D5AB52;  /* mustard — unused, available */
--c-olive:       #A19D6E;  /* muted olive — card-year text, avatar CB */
--c-sage:        #C5CDB1;  /* light sage — ambient, callout tints */
--c-forest:      #3F4F3D;  /* deep green — CTA buttons */

/* Neutrals */
--color-bg:        #f7f6f5;
--color-text:      #1a1a1a;
--color-muted:     #4a4a4a;
--color-faint:     #8a8a8a;
--color-border:    rgba(0,0,0,0.10);
--color-border-mid:rgba(0,0,0,0.18);
```

### Accent assignments (where each color goes)

| Element | Color |
|---|---|
| H1 italic `<em>` | `--c-rust` |
| Section labels (eyebrows like "SELECTED WORK") | `--c-brick` |
| Pull quotes / testimonial `<em>` | `--c-deep-blue` |
| Card arrow `↗` (default) | `--c-rust` |
| Card arrow `↗` (hover) | `--c-brick` |
| Card-year text | `--c-olive` |
| Card-tag pill (hover state) | `--c-steel` text + light steel bg |
| Nav link hover | `--c-terracotta` |
| Primary CTA button | `--c-forest` bg, hovers to `--c-olive` |
| Avatar TM | steel-blue tint |
| Avatar CB | olive |
| Avatar LX | brick on terracotta tint |
| Side-TOC active item | `--c-rust` (case studies — see audit) |

---

## Typography

- **Sans**: Karla (`'Karla', system-ui, sans-serif`)
- **Serif**: Crimson Pro (`'Crimson Pro', Georgia, serif`)
- **Body**: Karla 500, 15–16px, line-height 1.6, letter-spacing 0.01em
- **H1**: Crimson Pro 400, 50px (case studies) / 52px (homepage), italic em emphasis
- **H2**: Crimson Pro 400, 26–28px
- **Labels/eyebrows**: Karla 500, 10–11px, letter-spacing 0.10–0.12em, uppercase

Font import (every page):
```html
<link href="https://fonts.googleapis.com/css2?family=Crimson+Pro:ital,wght@0,300;0,400;0,500;0,600;1,400;1,500&family=Karla:ital,wght@0,300;0,400;0,500;1,400;1,500&family=Playfair+Display:wght@400;500&display=swap" rel="stylesheet" />
```

---

## Layout

- **Max-width**: `1060px` everywhere (`.wrap` on index/about, `.page` on case studies)
- **Horizontal padding**: `0 2rem`
- **Bottom padding** on index/about: `5rem`
- **Side TOC width** (case studies only): `190px`
- **Layout grid gap** (case studies): `5rem`

---

## Nav

**Locked: sticky, full-width, frosted glass** (the case-study pattern).

```css
nav {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 1.5rem 2rem;
  border-bottom: 0.5px solid var(--color-border);
  position: sticky;
  top: 0;
  background: rgba(247,246,245,0.92);
  backdrop-filter: blur(8px);
  -webkit-backdrop-filter: blur(8px);
  z-index: 100;
}
```

HTML: `<nav>` lives **outside** `.wrap` / `.page` so it spans the full viewport width.

```html
<body>
  <nav>...</nav>          <!-- outside, full-width -->
  <div class="wrap">      <!-- or <div class="page"> -->
    ...page content...
  </div>
</body>
```

- `.wrap` / `.page` should have `padding-top: 3rem` (case studies use `padding: 0 2rem` because hero has its own `padding: 5rem 0 3.5rem`)
- `.nav-name`: Crimson Pro 18px, "Shaade"
- `.nav-links`: 3 items — Work / About / Contact (LinkedIn external)
- Hover state: `--c-terracotta`
- Frosted bg matches `--color-bg` at 92% opacity so the texture below shows faintly through

---

## Background texture

Subtle 2-layer SVG noise on body, fixed-attachment so it acts like a wall texture, not scrolling content.

```css
body {
  background-color: var(--color-bg);
  background-image:
    /* fine dark specks */
    url("...feTurbulence 1.2, opacity 0.06..."),
    /* medium neutral grain */
    url("...feTurbulence 0.6, opacity 0.08...");
  background-attachment: fixed, fixed;
  background-size: 200px 200px, 240px 240px;
  background-repeat: repeat, repeat;
}
```

Same exact texture on every page. Don't tint warm or cool — keep neutral.

---

## Hero pattern (case studies)

```html
<header class="hero">
  <div class="hero-meta">
    <span class="hero-tag">Tag · Domain</span>
    <span class="hero-co">Company · Year</span>
  </div>
  <h1>Headline — <em>italic emphasis phrase</em></h1>
  <p class="hero-sub">Lead paragraph, 1–3 sentences.</p>
</header>

<div class="summary">
  <div class="s-item"><p class="s-label">Role</p><p class="s-val">…</p></div>
  <div class="s-item"><p class="s-label">Scope</p><p class="s-val">…</p></div>
  <div class="s-item"><p class="s-label">Outcome</p><p class="s-val">…</p></div>
  <div class="s-item"><p class="s-label">Type</p><p class="s-val">…</p></div>
</div>
```

- `.hero-meta` is a small inline pill-tag + dim co/year line — NOT a 4-column grid
- `.summary` is the 4-column metadata block, separate from hero
- `.s-item` background = `var(--color-bg)` (#f7f6f5) — seamless, no white islands
- No breadcrumb (was deprecated)
- No top-level stat-band (stats live inside relevant section instead)

---

## Section pattern (case studies)

```html
<section class="section" id="problem">
  <p class="sec-label">The Problem</p>
  <h2>Section heading.</h2>
  <p>…</p>
</section>
```

- **No section numbers** (01, 02…). Use text eyebrows like "The Problem", "Research", "Outcome".
- Sections live inside `<div class="layout">` with `<aside class="side">` (sticky right TOC).

---

## Component snippets

| Component | Usage |
|---|---|
| `.callout` | Quote-style emphasis, left-border 2px `--color-text` |
| `.insight` | Sidebar pull-quote in 3fr/2fr layouts, serif text |
| `.prob-list` | Em-dash bullet list |
| `.research-grid` / `.rq-card` | 2-column research-question cards |
| `.wf-steps` / `.wf-step` | 3-column workflow cards with serif numbers |
| `.ba-grid` | Before / after pair (warm/cool labels) |
| `.outcome-grid` | 2x2 reflection cards at end of case study |
| `.img-wrap` | Inline image container with hairline border |

---

## Audit checklist (per page)

- [ ] Palette tokens present in `:root`
- [ ] Body bg = `#f7f6f5` with 2-layer texture applied
- [ ] Karla + Crimson Pro fonts loaded
- [ ] Max-width 1060px
- [ ] Nav matches the in-wrap pattern (not sticky/frosted)
- [ ] H1 italic em uses `--c-rust`
- [ ] Section labels use `--c-brick`
- [ ] `.s-item` bg matches page bg (no white islands)
- [ ] No breadcrumb in hero
- [ ] No section numbers (01/02/…)
- [ ] Case-nav footer present

---

## Pages that don't yet match this guide

| Page | What's off |
|---|---|
| `work-admin-grid.html` | 900px wrap, breadcrumb hero, numbered sections, in-hero meta grid |
| Case studies (some) | `.s-item` bg = `#fff` instead of `#f7f6f5` (creates white islands on summary) |
| Case studies (some) | Nav `background: rgba(255,255,255,0.95)` — should be `rgba(247,246,245,0.92)` to match cream bg |

Fix these one page at a time, verifying against the checklist above.

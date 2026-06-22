# Claude Code Handoff — Admin Grid Case Study
## work-admin-grid.html

This document gives Claude Code everything needed to update the Admin Grid case study page to match the portfolio styleguide and integrate new components and copy.

---

## What this page is

A portfolio case study for the Admin Grid Console Overhaul at UserVoice. The page already exists at `work-admin-grid.html` with full content, but it has known spec issues and needs new components, updated copy, and a visual layout overhaul.

---

## Known issues to fix first

Per the styleguide audit checklist, `work-admin-grid.html` currently has:

- **Wrong max-width** — page is using `900px` wrap, should be `1060px` (`.wrap` or `.page`)
- **Breadcrumb** — styleguide says remove, delete it
- **Numbered sections** — styleguide says remove section numbers (01, 02, 03 etc.), delete them
- **Nav** — not sticky/frosted glass, needs to match the global nav pattern from other pages
- **Any inline styles** — move to the `<style>` block

Fix these before doing anything else.

---

## Fonts and CSS variables

Every page loads these from Google Fonts in `<head>`:
```html
<link href="https://fonts.googleapis.com/css2?family=Karla:wght@400;500;600;700&family=Crimson+Pro:ital,wght@0,400;0,600;1,400&display=swap" rel="stylesheet">
```

CSS variables are defined in `:root` — copy them from another case study page (e.g. `work-idea-sheet.html`) and paste into the `<style>` block of this page. Do not hardcode colors.

Key variables to use:
- `--font-sans`: Karla
- `--font-serif`: Crimson Pro  
- `--wrap`: 1060px max-width
- `--text`, `--text-muted`, `--text-dim`: text colors
- `--bg`, `--bg-2`, `--bg-3`: background levels
- `--border`: border color
- `--blue`, `--red`, `--green`: accent colors

---

## Page layout

The case study uses a two-column layout:
```css
.layout {
  display: grid;
  grid-template-columns: 1fr 140px;
  gap: 0 48px;
  align-items: start;
}
```

Left column: all content sections
Right column: sticky TOC sidebar with anchor links to each section

The TOC should have anchor links to each major section. Update the TOC to match the new section structure below.

---

## New section structure

Replace the existing section content with this structure (in order):

### Hero
- Full-width header with title: **"From looking at ideas to doing something with them"**
- Subtitle: "The Idea Grid was UserVoice's most-visited surface — over a million page views a year, 60% of all admin interactions. It was also running on a legacy architecture where every filter, sort, and click triggered a full page reload. I used performance as the strategic wedge to get this work resourced, then designed a foundation that the product grew into for the next two years."
- Meta strip: Role (Sole product designer) · Platform (Admin Console) · Cycle (6 weeks) · What followed (Idea Lists → Themes → Impact Reports)
- Stat band: three stats — `1M+` page views / `3.6s` grid load / `60%` of admin interactions

### Before/After Slider
- Use the `.ba-strip` / `.ba-panel` component classes from the styleguide
- Integrate the slider JS/CSS from `grid-slider.html` (see Assets section below)
- Images: `/images/grid-before.png` and `/images/grid-after.png`
- Label "Before" left, "After" right, drag handle in center
- Caption below: "Drag to compare — the old Angular grid vs the redesigned React grid"

### The setup *(no number, no breadcrumb)*
Copy:
> The Idea Grid had been built over years in a legacy architecture where every filter, sort, and click triggered a full page reload. Not a component update — the whole page. Filtering took 3.5 seconds. Sorting took 2. Grid load: 3.6 seconds. "Let's modernize the grid" doesn't get resourced. I needed a sharper wedge.

### The problem you couldn't pitch directly
Copy from `admin-grid-case-study.md` — section 01.

Include the **performance table** directly below the opening paragraph:

| Core action | UserVoice | Productboard | Target |
|---|---|---|---|
| Grid load | 3.6s | 1.75s | 1.0s |
| Applying filters | ~3.5s | 0.10s | 0.10s |
| Sorting | 2.0s | 0.10s | 0.10s |
| Idea detail open | 2.7s | 0.30s | 1.0s |

Caption: *NNG threshold: under 1s feels responsive. Over 3s, flow breaks. Most of our core actions were in the wrong zone.*

Then place the **before image** full-width below the table:
```html
<div class="img-wrap">
  <img src="/images/grid-before.png" alt="The old Admin Grid — horizontal scroll, bar chart visualizations, no filter state visibility">
  <p class="img-caption">The old Angular grid — every core action taking 3+ seconds, reach column bar charts adding noise, filter state invisible at a glance.</p>
</div>
```

### How I approached it
Use `.callout` or a styled list for the five methodology principles. Each is **bold label** followed by one sentence. Copy from `admin-grid-case-study.md` — section 02.

### What users actually needed
Copy from `admin-grid-case-study.md` — section 03.

Pull quotes use `.research-cards` or equivalent quote component from styleguide:
- "The less she has to do page loads, the better." — Power User, Procore
- "The new color scheme makes it clear to see and the slide out filter list is easy to use. I like the idea of mass selection for tasks." — Product Manager, ShowingTime

### The design bet: a slideout for everything
Copy from `admin-grid-case-study.md` — section 04.

Place the **filter system image** full-width after the opening paragraphs:
```html
<div class="img-wrap">
  <img src="/images/grid-filter-system.png" alt="Filter system across all states">
  <p class="img-caption">Filter system mapped across all states — top-level entry, parent/child nesting up to three levels, expanded states for large taxonomies, and per-column mini filters.</p>
</div>
```

Third pull quote below filter image:
- "Forum and category filters worked better when they were above the ideas heading — all the filters were clearly visible. Having them hidden can cause confusion." — Product Manager, SimplePractice

### What shipped
**This section uses the circle grid component** — do not use a standard list or prose here.

Integrate the circle grid from `shipped-circles.html` (see Assets). Extract just the `.grid` and `.card` HTML + CSS and drop it in as a component inside this section. Remove the outer `<body>` wrapper.

Images for each circle are referenced from `/images/` — see image mapping below.

The six items:
1. Flexible columns → `/images/circle-columns.png`
2. Filter drawer → `/images/circle-filter.png`
3. Bulk actions → `/images/circle-bulk.png`
4. Color as wayfinding → `/images/circle-color.png`
5. Strategic subtraction → `/images/circle-subtraction.png`
6. Built to extend → `/images/circle-extend.png`

After the circle grid, place the **nav bar states image**:
```html
<div class="img-wrap">
  <img src="/images/grid-nav-states.png" alt="Navigation bar states across all breakpoints">
  <p class="img-caption">Navigation bar in all states — default, saved view, edit mode, responsive from 1200px down to 400px.</p>
</div>
```

Then the **Custom Fields + column picker image**:
```html
<div class="img-wrap">
  <img src="/images/grid-custom-fields.png" alt="Column picker open with Custom Fields visible">
  <p class="img-caption">The column picker open alongside the grid — Custom Fields, inline label editing, urgency scale. The forward-thinking component decisions made real.</p>
</div>
```

Then the **column library image**:
```html
<div class="img-wrap">
  <img src="/images/grid-column-library.png" alt="Every column type designed to spec">
  <p class="img-caption">Every column type designed to spec — Activity, Merge Match, Labels + Inline Editing, Importance, Salesforce, Reach, Jira, Azure, Custom Segment, and more.</p>
</div>
```

### What the grid made possible
Copy from `admin-grid-case-study.md` — section 06.

Place **bulk action slideout image** after describing the pattern evolution:
```html
<div class="img-wrap">
  <img src="/images/grid-bulk-slideout.png" alt="Bulk action slideout with full action set">
  <p class="img-caption">The bulk action slideout — the interaction pattern that grew from the initial bottom bar — now containing Label, Merge, Move, Custom Field, Internal/Public Status, and Add to Idea List.</p>
</div>
```

Close the section with the **themes panel image** as the final visual:
```html
<div class="img-wrap">
  <img src="/images/grid-themes.png" alt="Grid with AI theme detection panel open">
  <p class="img-caption">The grid with AI-powered theme detection — the arc made visible in a single frame. Grid → Idea Lists → Themes → Impact Reports.</p>
</div>
```

### What I'd tell you
Copy from `admin-grid-case-study.md` — section 07. Three bold takeaways, no numbered list.

---

## Assets to move into /images/

Copy these files into the `/images/` directory and rename as follows:

| Source file | Rename to |
|---|---|
| `grid_before.png` | `grid-before.png` |
| `Frame_7098_1.png` | `grid-after.png` |
| `Screenshot_2026-06-18_at_1_28_57_PM.png` | `grid-nav-states.png` |
| `Screenshot_2026-06-18_at_1_37_56_PM.png` | `grid-filter-system.png` |
| `Frame_7011.png` | `grid-column-library.png` |
| `CFs.png` | `grid-custom-fields.png` |
| `Frame_21665.png` | `grid-bulk-slideout.png` |
| `Frame_1000000909.png` | `grid-themes.png` |
| `circle_columns.png` | `circle-columns.png` |
| `circle_filter.png` | `circle-filter.png` |
| `circle_bulk.png` | `circle-bulk.png` |
| `circle_color.png` | `circle-color.png` |
| `circle_subtraction.png` | `circle-subtraction.png` |
| `circle_extend.png` | `circle-extend.png` |

---

## Components to integrate

### Before/After Slider
Source: `grid-slider.html`

Extract:
- The CSS from the `<style>` block (`.slider-container`, `.img-before-wrap`, `.img-before`, `.img-after`, `.divider`, `.handle`)
- The JS from the `<script>` block
- The HTML structure inside `.wrapper`

Replace the base64 image sources with file references:
```html
<img class="img-after" src="/images/grid-after.png" ...>
<img class="img-before" src="/images/grid-before.png" ...>
```

Adapt class names to avoid conflicts with existing styleguide classes. Prefix with `ba-` if needed (`.ba-slider-container`, `.ba-handle`, etc.) — check styleguide for existing `.ba-` usage first.

### Circle Grid
Source: `shipped-circles.html`

Extract:
- The CSS (`.grid`, `.card`, `.circle-wrap`, `.card-label`, `.card-desc`)
- The HTML grid markup

Replace base64 image sources with file references from `/images/circle-*.png`.

Adapt class names if `.grid` or `.card` conflict with existing styleguide classes — prefix with `.shipped-` if needed.

---

## Copy source

All prose copy lives in `admin-grid-case-study.md`. Use it as the source of truth. Do not invent or paraphrase — copy exactly.

The visual layout reference doc `admin-grid-visual-layout.docx` shows every image placed in context with captions — use it as a visual reference for placement decisions.

---

## TOC sidebar

Update the sticky TOC to match the new sections:
- The setup
- The problem
- How I approached it
- What users needed
- The design bet
- What shipped
- What it made possible
- What I'd tell you

Each TOC item is an anchor link to the corresponding section `id`.

---

## Things NOT to change

- The overall page shell (html, head, meta tags, font loading)
- The global nav structure — just make it sticky/frosted to match spec
- Any existing `.outcome-rows` or footer patterns already in spec
- The next/previous case study navigation at the bottom if it exists

---

## Definition of done

- [ ] Page uses 1060px max-width
- [ ] Nav is sticky with frosted glass effect
- [ ] No breadcrumb
- [ ] No numbered sections
- [ ] All CSS variables from `:root`, no hardcoded colors
- [ ] Karla and Crimson Pro loaded and applied correctly
- [ ] Two-column layout with sticky TOC sidebar
- [ ] Before/after slider works, images load from `/images/`
- [ ] Circle grid renders correctly, all 6 circles visible
- [ ] All 8 full-width images placed with captions
- [ ] Performance table styled and readable
- [ ] Three pull quotes styled per styleguide quote component
- [ ] Copy matches `admin-grid-case-study.md` exactly
- [ ] Page is responsive down to mobile (single column, TOC collapses)
- [ ] No inline styles remaining

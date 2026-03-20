# Clinom-X Research Project — Static Website Specification
**Version:** 1.0  
**Target:** Coding agent (pure HTML5 + CSS3, no JavaScript frameworks, no build tools)  
**Output:** A self-contained multi-page static site deployable on any static host (GitHub Pages, Netlify, plain web server)

---

## 1. Project Overview

**Site name:** Clinom-X  
**Nature:** Academic / medical research project presentation site  
**Audience:** Clinicians, researchers, medical AI professionals, institutional partners  
**Tone:** Authoritative, modern, clear — editorial-scientific register  
**Language:** English (internationalisation hooks not required at this stage)

---

## 2. File & Directory Structure

```
clinom-x/
├── index.html          # Homepage
├── events.html         # Events list
├── people.html         # Team / contributors
├── links.html          # External resources & links
├── css/
│   └── style.css       # Single shared stylesheet
├── img/
│   ├── logo.svg        # Project logo (placeholder vector)
│   └── hero-bg.svg     # Hero background pattern (SVG noise/grid)
└── favicon.ico         # 32×32 favicon (placeholder)
```

All pages share `css/style.css`. No JavaScript is required; CSS-only interactions (`:hover`, `:focus`, smooth scrolling via `scroll-behavior: smooth`) are permitted and encouraged.

---

## 3. Design System

### 3.1 Aesthetic Direction

**Concept:** "Precision Instrument" — the visual language of high-resolution scientific equipment. Refined, dark-first, with cold-white typography on deep navy/charcoal ground. Geometric precision, micro-ruled grid lines as decorative motifs, sharp contrast accents.

Not a generic corporate site. Not purple-gradient SaaS. Think: a Nature paper cover crossed with a monochrome instrument dashboard.

### 3.2 Color Palette (CSS custom properties)

```css
:root {
  --clr-bg:          #0b0f1a;   /* Deep navy-black — page background        */
  --clr-surface:     #131928;   /* Slightly lifted surface — cards, panels   */
  --clr-border:      #1e2a40;   /* Subtle ruled lines / dividers             */
  --clr-accent:      #3b82f6;   /* Electric blue — primary action / highlight*/
  --clr-accent-dim:  #1d4ed8;   /* Darker accent for hover states            */
  --clr-text:        #e2e8f0;   /* Primary text                              */
  --clr-text-muted:  #64748b;   /* Secondary / meta text                     */
  --clr-text-bright: #f8fafc;   /* Headings, hero                            */
  --clr-tag-bg:      #1e3a5f;   /* Chip / tag background                     */
  --clr-tag-text:    #93c5fd;   /* Chip / tag text                           */
  --clr-rule:        #1e2a40;   /* HR / table border color                   */
}
```

### 3.3 Typography

Load from Google Fonts with a single `<link>` in `<head>`:

```html
<link href="https://fonts.googleapis.com/css2?family=DM+Serif+Display:ital@0;1&family=IBM+Plex+Mono:wght@400;500&family=Inter:wght@300;400;500;600&display=swap" rel="stylesheet">
```

| Role | Family | Weight | Usage |
|---|---|---|---|
| Display / Hero | `DM Serif Display` | 400, italic | Page titles, hero headline |
| Body | `Inter` | 300, 400, 500, 600 | All body copy, navigation |
| Monospace / accent | `IBM Plex Mono` | 400, 500 | Labels, tags, metadata, breadcrumbs |

**Scale (rem):**
- `--fs-xs: 0.75rem` — captions, meta
- `--fs-sm: 0.875rem` — secondary text, nav
- `--fs-base: 1rem` — body
- `--fs-lg: 1.125rem` — subheadings
- `--fs-xl: 1.5rem` — section titles
- `--fs-2xl: 2rem` — page titles
- `--fs-hero: clamp(2.5rem, 6vw, 5rem)` — hero headline

### 3.4 Layout Grid

- Max content width: `1100px`, centred with `margin-inline: auto`
- Page padding: `padding-inline: clamp(1rem, 5vw, 3rem)`
- Sections use `padding-block: 4rem`
- Card grids: CSS Grid, `repeat(auto-fill, minmax(300px, 1fr))`, gap `1.5rem`
- The layout uses a **fixed left vertical rule** (a 1px solid `var(--clr-border)` absolutely positioned at ~`4rem` from left, `100vh` tall, as a pure CSS decorative device on `>1024px` screens)

### 3.5 Decorative Motifs

- SVG inline `<pattern>` background in the hero: a subtle dot-matrix grid (dots `1px`, spacing `24px`, colour `rgba(59,130,246,0.08)`)
- Section separators: `<hr>` styled as `border: none; border-top: 1px solid var(--clr-rule)` with `margin-block: 3rem`
- Cards: `border: 1px solid var(--clr-border)`, `border-radius: 6px`, no box-shadow by default; on `:hover` apply `border-color: var(--clr-accent)` and a subtle `box-shadow: 0 0 0 1px var(--clr-accent)`
- All transitions: `transition: all 0.2s ease`

---

## 4. Shared Components

### 4.1 `<head>` Block (all pages)

```html
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<meta name="description" content="Clinom-X — [page-specific description]">
<title>Clinom-X | [Page Name]</title>
<link rel="stylesheet" href="css/style.css">
<!-- Google Fonts -->
```

### 4.2 Site Header / Navigation

**Structure:** Fixed-top `<header>` with `backdrop-filter: blur(12px)` and `background: rgba(11,15,26,0.85)`. Height `64px`. Contains:

- **Left:** Logo mark (inline SVG hexagon glyph in accent blue) + `CLINOM-X` in `IBM Plex Mono` weight 500, letter-spacing `0.12em`, colour `--clr-text-bright`
- **Center:** `<nav>` with four links:
  - `Home` → `index.html`
  - `Events` → `events.html`
  - `People` → `people.html`
  - `Links` → `links.html`
- **Right:** A "Contact" CTA button (small, `border: 1px solid var(--clr-accent)`, `color: var(--clr-accent)`, `border-radius: 4px`, `padding: 0.35rem 0.9rem`, `font-family: IBM Plex Mono`)

Navigation links: `font-size: var(--fs-sm)`, `font-family: Inter`, weight 500, uppercase, letter-spacing `0.06em`, colour `--clr-text-muted`; on `:hover` and `.active` → `--clr-text-bright`

The active page's nav link gets class `active` (set manually per page).

**Mobile:** Below `768px`, nav collapses to a CSS-only drawer using a hidden checkbox + `<label>` hamburger toggle. The menu opens as a full-width vertical list, `position: fixed`, `top: 64px`, `background: var(--clr-bg)`.

### 4.3 Site Footer

Full-width `<footer>`, `border-top: 1px solid var(--clr-border)`, `padding-block: 2.5rem`, two-column flex:

- **Left:** `© 2025 Clinom-X Research Consortium` in `IBM Plex Mono`, `--clr-text-muted`, `--fs-xs`
- **Right:** Repeated four nav links in `--fs-xs`

---

## 5. Page Specifications

---

### 5.1 Homepage — `index.html`

**Purpose:** First impression. Communicate what Clinom-X is, its scientific rationale, key objectives, and invite further exploration.

#### Section A — Hero

Full-viewport-height (`min-height: 100svh`) section. Background: inline SVG dot-grid pattern over `--clr-bg`. Layout: vertically centred flex column, left-aligned text, max-width `700px`.

Content elements (in order):
1. **Eyebrow label:** `IBM Plex Mono`, `--fs-xs`, `--clr-accent`, uppercase, letter-spacing `0.15em` → `RESEARCH PROJECT · 2024–2027`
2. **Headline:** `DM Serif Display`, `--fs-hero`, `--clr-text-bright`, line-height `1.1` → `Clinom-X`
3. **Tagline:** `DM Serif Display` italic, `clamp(1.25rem, 3vw, 1.75rem)`, `--clr-text-muted` → `[One-sentence description of the project — placeholder: "Advancing clinical decision support through probabilistic knowledge graphs and interpretable AI."]`
4. **Abstract paragraph:** `Inter` 300, `--fs-base`, `--clr-text`, max 3 sentences → `[Project abstract placeholder]`
5. **CTA row:** Two buttons side by side
   - Primary: filled `--clr-accent` bg, white text, `Learn More` → `#about`
   - Secondary: outlined as nav CTA → `View Events` → `events.html`
6. **Scroll indicator:** A small animated CSS downward chevron at bottom-center of hero

#### Section B — About (`id="about"`)

Two-column layout (`60% / 40%`), below `768px` single column.

- **Left:** `<h2>` ("About the Project") + 3–4 paragraphs of body text (placeholder). Include a `<blockquote>` styled with a `4px` left border in `--clr-accent`, italic text.
- **Right:** A "Key Facts" card (`--clr-surface` background, `border: 1px solid var(--clr-border)`) listing 4–5 items in a definition-list (`<dl>`) style:
  - Duration, Funding body, Lead institution, Methodology, Status
  - `<dt>` in `IBM Plex Mono` `--fs-xs` `--clr-text-muted` uppercase
  - `<dd>` in `Inter` weight 500 `--clr-text-bright`

#### Section C — Objectives

`<h2>` ("Objectives") + a CSS Grid `repeat(auto-fill, minmax(280px, 1fr))` of **Objective Cards**. Each card:
- Number badge: `IBM Plex Mono`, large `--clr-accent`, `opacity: 0.3`, absolute top-right
- Short title: `Inter` 600
- One-sentence description: `Inter` 300 `--clr-text-muted`
- `border: 1px solid var(--clr-border)`, hover → `border-color: var(--clr-accent)`

Provide 4 placeholder objective cards.

#### Section D — Latest Events (preview strip)

`<h2>` ("Recent Events") + a horizontal 3-card flex row (overflow-x: auto on mobile) showing the 3 most recent events as compact cards. Each card links to `events.html`. A "View all events →" text link below.

#### Section E — Partners / Affiliations

Centred section, `<h3>` ("Institutional Partners") + a flex-wrap row of **institution placeholder boxes** (outlined rectangles with centred `[Institution Name]` text in `--clr-text-muted`). 5–6 placeholders.

---

### 5.2 Events Page — `events.html`

**Purpose:** Chronological list of project-related events (conferences, workshops, seminars, deliverable milestones, publications).

#### Page Header

Narrow hero band (`min-height: 220px`): eyebrow + `<h1>` ("Events") + one-sentence description. No full-viewport height.

#### Filter Bar

A CSS-only visual filter bar (no JS — purely decorative tabs, the filtering itself can be noted as a future JS enhancement). Three labelled pills: `All · Conferences · Publications · Milestones`. Styled using `<ul>` + `<li>` + `<a>` with `--clr-surface` background, active pill gets `--clr-accent` border-bottom.

#### Events List

A vertical `<ul>` timeline. Each `<li>` is an **Event Entry**:

```
[Year column]  |  [Content column]
```

- Left column (80px, right-aligned): Year in `IBM Plex Mono` `--clr-accent`
- Vertical rule: `1px solid var(--clr-border)`
- Right column:
  - **Date line:** `IBM Plex Mono` `--fs-xs` `--clr-text-muted` — full date, e.g. `12 Mar 2025`
  - **Type tag / chip:** inline pill, e.g. `CONFERENCE`, `PUBLICATION`, `MILESTONE` — `--clr-tag-bg` bg, `--clr-tag-text` text, `IBM Plex Mono` `--fs-xs`
  - **Title:** `Inter` weight 600 `--clr-text-bright` `--fs-lg`
  - **Location / venue:** `Inter` 400 `--clr-text-muted` `--fs-sm`
  - **Short description:** `Inter` 300 `--clr-text` `--fs-base` (1–2 sentences)
  - **Optional link:** `[→ Abstract / Programme]` as a small `--clr-accent` text link

Provide **8 placeholder events** spanning 2024–2026, mix of all three types.

---

### 5.3 People Page — `people.html`

**Purpose:** Present all members of the research consortium — PIs, postdocs, engineers, clinical partners.

#### Page Header

Same narrow hero band as Events page. `<h1>` ("People") + subtitle.

#### Group Sections

Organise by role group, each introduced by a `<h2>` with a small `IBM Plex Mono` label above it (e.g., `PRINCIPAL INVESTIGATORS`, `RESEARCHERS & ENGINEERS`, `CLINICAL PARTNERS`, `ADVISORY BOARD`).

#### Person Card Grid

CSS Grid `repeat(auto-fill, minmax(240px, 1fr))` of **Person Cards**. Each card (`--clr-surface`, `border: 1px solid var(--clr-border)`, `border-radius: 6px`, `padding: 1.5rem`):

- **Avatar placeholder:** A `64px × 64px` circle, `background: var(--clr-border)`, centred initials in `IBM Plex Mono` `--clr-accent`
- **Name:** `Inter` 600 `--clr-text-bright`
- **Role / title:** `Inter` 400 `--fs-sm` `--clr-text-muted`
- **Affiliation:** `IBM Plex Mono` `--fs-xs` `--clr-text-muted`
- **Bio snippet:** 1–2 sentences, `Inter` 300 `--fs-sm` `--clr-text`
- **Icon links row:** Three small icon-buttons (`[✉]` email, `[i]` ORCID, `[↗]` personal page) — use Unicode symbols or inline SVG; `--clr-text-muted`, `:hover → --clr-accent`

Provide **10 placeholder people** across the four groups (3 PIs, 4 researchers, 2 clinical partners, 1 advisor).

---

### 5.4 Links Page — `links.html`

**Purpose:** Curated directory of external resources relevant to the project.

#### Page Header

Narrow hero band. `<h1>` ("External Resources") + subtitle.

#### Link Categories

Organise into titled sections using `<h2>` + `<ul>` of **Link Entries**. Categories:

1. **Project Infrastructure** — repositories, data portals, preregistration
2. **Key Publications** — seminal papers relevant to the project's domain
3. **Tools & Frameworks** — software, ontologies, databases used
4. **Partner Institutions** — institutional home pages
5. **Funding & Policy** — grant portals, regulatory documents

#### Link Entry

Each `<li>` rendered as a horizontal card (`display: flex`, `padding: 1rem 1.25rem`, `border: 1px solid var(--clr-border)`, `border-radius: 4px`, `margin-bottom: 0.5rem`):

- **Left icon area (40px):** Category icon using a Unicode emoji or inline SVG (e.g., `⬡` for data, `◎` for publication)
- **Main content:**
  - **Title:** `Inter` 600 `--clr-text-bright` — the resource name
  - **URL preview:** `IBM Plex Mono` `--fs-xs` `--clr-text-muted` — truncated domain
  - **Description:** `Inter` 300 `--fs-sm` `--clr-text` — one sentence
- **Right:** External link icon `↗` in `--clr-accent`; entire card is an `<a>` wrapping the li content with `target="_blank" rel="noopener noreferrer"`

On `:hover`: `border-color: var(--clr-accent)`, background `--clr-surface`.

Provide **15 placeholder links** distributed across categories.

---

## 6. CSS Architecture

All styles in a **single `css/style.css`** file, structured as follows:

```
/* =========================================================
   0. Custom Properties (Design Tokens)
   ========================================================= */

/* =========================================================
   1. CSS Reset / Base
   ========================================================= */
/* Modern minimal reset: box-sizing, margin/padding 0,
   img max-width, line-height inheritance */

/* =========================================================
   2. Base Typography
   ========================================================= */
/* body font, heading defaults, link defaults */

/* =========================================================
   3. Layout Utilities
   ========================================================= */
/* .container, .section, .grid-auto, .flex-row, .sr-only */

/* =========================================================
   4. Components
   ========================================================= */
/* 4.1 Header / Nav
   4.2 Footer
   4.3 Hero
   4.4 Cards (generic)
   4.5 Buttons
   4.6 Tags / Chips
   4.7 Timeline (events)
   4.8 Person Card
   4.9 Link Entry
   4.10 Blockquote
   4.11 Horizontal Rule */

/* =========================================================
   5. Pages
   ========================================================= */
/* 5.1 Homepage sections
   5.2 Events page
   5.3 People page
   5.4 Links page */

/* =========================================================
   6. Responsive (Mobile-first breakpoints)
   ========================================================= */
/* @media (min-width: 768px) {}
   @media (min-width: 1024px) {} */

/* =========================================================
   7. Animations & Transitions
   ========================================================= */
/* Fade-in on load via @keyframes, CSS custom scroll hint */
```

**No CSS preprocessors. No utility frameworks. No external CSS libraries.**

---

## 7. Accessibility & Quality Requirements

| Requirement | Implementation |
|---|---|
| Semantic HTML | Use `<header>`, `<nav>`, `<main>`, `<section>`, `<article>`, `<footer>`, `<h1>`–`<h3>` hierarchy |
| Colour contrast | All text/bg pairs must meet WCAG AA (4.5:1 for body, 3:1 for large text) |
| Focus styles | Custom `:focus-visible` outline in `--clr-accent`, `outline-offset: 3px` |
| Alt text | All `<img>` carry descriptive `alt` attributes; decorative SVGs get `aria-hidden="true"` |
| Skip link | `<a class="skip-link" href="#main">Skip to content</a>` as first element in body, visually hidden until focused |
| External links | All `target="_blank"` links include `rel="noopener noreferrer"` and a visually hidden ` (opens in new tab)` span |
| Print styles | A minimal `@media print {}` block: hide nav/footer, show link URLs via `a::after { content: " (" attr(href) ")"; }` |
| Viewport units | Use `svh`/`svw` for mobile-safe viewport units in hero; fallback to `vh`/`vw` |

---

## 8. Placeholder Content Guidelines

The agent must populate all pages with **realistic, domain-appropriate placeholder content** rather than "Lorem ipsum":

- Project description → AI-assisted clinical decision support for rare/complex disease workup
- Objectives → e.g., "Develop a validated probabilistic knowledge graph", "Evaluate explainability metrics in GP settings", etc.
- Events → Mix of ECAI 2025, AIME 2025, JAMIA submission, consortium kickoff, etc.
- People → Fictional but plausible names, realistic titles (PI, postdoc, clinical informatician), real-sounding European institutions
- Links → Use real-domain placeholders (e.g., `orphanet.org`, `hpo.jax.org`, `github.com/clinom-x`, `cordis.europa.eu`) with descriptive text

---

## 9. Deliverables Checklist

The agent must produce the following files, all functionally complete:

- [ ] `index.html` — Homepage (all 5 sections)
- [ ] `events.html` — Events page (8 entries)
- [ ] `people.html` — People page (10 people, 4 groups)
- [ ] `links.html` — Links page (15 entries, 5 categories)
- [ ] `css/style.css` — Complete shared stylesheet (~600–900 lines)
- [ ] `img/logo.svg` — Inline-compatible SVG logo placeholder
- [ ] `img/hero-bg.svg` — Dot-grid SVG pattern
- [ ] `favicon.ico` — Minimal placeholder (16×16 or 32×32)

The site must render correctly with no broken links between pages. All pages must pass HTML5 validation (W3C-compatible markup). The stylesheet must contain no vendor-specific hacks beyond `webkit` prefixes for backdrop-filter.

---

## 10. Non-Goals (Out of Scope for this Version)

- JavaScript interactivity (search, filtering, dark/light toggle)
- CMS integration or templating engines
- Build pipeline (Webpack, Vite, etc.)
- Internationalisation / multi-language support
- Dynamic content (server-side rendering, API calls)
- Authentication or user accounts
# CLINOM-X — Static Website

**Site name:** CLINOM-X
**Nature:** Academic / medical research project presentation site
**Institution:** UCLouvain — ICTEAM Institute (Belgium)
**Technology:** Pure HTML5 + CSS3, no JavaScript frameworks, no build tools
**Deployment:** Self-contained multi-page static site deployable on any static host

---

## Project Description

CLINOM-X is a research project developing a decentralized IT infrastructure for secure management of clinomic data for biomedical research. By clinomic data we mean the multimodal combination of clinical, biological, behavioural, neurophysiological, anatomopathological, multi-omic (genomic, transcriptomic, proteomic, metabolomic), and imaging data.

The project is developed at UCLouvain (Belgium), in the ICTEAM research institute, and is part of the WAL-IMAGIN portfolio (MedReSyst). Financial support is provided by WalEurope (ERDF + Wallonia) and En Mieux.

---

## File & Directory Structure

```
claudomix/
├── index.html                          # Homepage
├── events.html                         # Events timeline (with CSS-only filtering)
├── people.html                         # Team / contributors
├── links.html                          # External resources & links
├── css/
│   └── style.css                       # Single shared stylesheet
├── img/
│   ├── logo.svg                        # Project logo (SVG hexagon)
│   ├── hero-bg.svg                     # Hero background dot-grid pattern
│   ├── logo_UCLouvain_format_jpg_RVB.jpg  # UCLouvain logo
│   ├── logo_UE+wallonie+FWB.jpg        # Funding partners logos
│   └── peoples/
│       ├── jodogne.jpg                 # Prof. Sébastien Jodogne
│       ├── roucoux.jpg                 # François Roucoux
│       ├── molka.jpg                   # Molka Anaghim Ftouhi
│       └── schmitz.jpg                 # Donatien Schmitz
└── favicon.ico                         # 16×16 favicon
```

---

## Pages

### Homepage — `index.html`

- **Hero** — Project name, tagline, abstract, CTA buttons, and Key Facts card (side-by-side on desktop)
- **About** — Context on growing biomedical data, the hospital access challenge, and CLINOM-X's role
- **Objectives** — 4 cards: decentralized infrastructure, secure external access, hospital dashboard, AI/analysis foundation
- **Recent Events** — 3 preview cards linking to the events page
- **Partners & Funding** — UCLouvain logo (linked to ICTEAM) and funding partners logos (En Mieux, EU/ERDF, Wallonie, FWB)

### Events — `events.html`

- Chronological timeline of project events (conferences, workshops, publications, milestones)
- **CSS-only filtering** using radio inputs and sibling selectors (no JavaScript)
- Filter categories: All, Conferences, Workshops, Publications, Milestones

### People — `people.html`

- **Project Promotor & Advisor** — Prof. Sébastien Jodogne (with photo)
- **Researchers & Engineers** — François Roucoux (main investigator), Molka Anaghim Ftouhi (software engineer), Donatien Schmitz (postdoctoral researcher)

### Links — `links.html`

Curated directory of external resources across 5 categories:

1. **Project Infrastructure** — UCLouvain Forge repository, MedReSyst Med Smart Factory
2. **Key Publications** — MIE 2026 paper (DIAL repository)
3. **Tools & Frameworks** — HPO, Orphanet, SNOMED CT
4. **Partner Institutions** — UCLouvain/ICTEAM, MedReSyst
5. **Funding** — En Mieux, WalEurope, European Commission

---

## Design System

- **Theme:** Light background (`#f8f9fb`) with dark text, blue accent (`#2563eb`)
- **Typography:** DM Serif Display (headings), Inter (body), IBM Plex Mono (labels/tags) — loaded from Google Fonts
- **Layout:** Max width `1100px`, responsive with breakpoints at `768px` and `1024px`
- **Components:** Fixed header with backdrop blur, CSS-only mobile hamburger menu, fixed Contact button, card system, timeline, person cards with photos
- **Accessibility:** Skip link, `:focus-visible` styles, semantic HTML, WCAG AA contrast, `aria` attributes, print stylesheet

---

## Contact

François Roucoux — [francois.roucoux@uclouvain.be](mailto:francois.roucoux@uclouvain.be)

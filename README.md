# Lux Christi — Software Engineering Learning & Building Blueprint

A static, responsive reference website that maps the journey from beginner to professional software engineer, with **Lux Christi** as the long-term project laboratory.

It answers one question:

> "What do I need to learn, in what order, and how will that knowledge eventually enable me to professionally design, build, secure, test, deploy and scale Lux Christi?"

**This website is NOT the Lux Christi application.** It is a blueprint.

> This website intentionally uses only HTML5, CSS3 and Vanilla JavaScript. No framework, library, backend or database is required.

---

## Technology used

| Layer | What is used |
|---|---|
| Structure | HTML5, semantic elements, accessible markup |
| Styling | CSS3 — variables, Flexbox, Grid, media queries, light transitions |
| Behaviour | Vanilla JavaScript (modern ES) — DOM manipulation and event handling only |

Not used, on purpose: React, Vue, Tailwind, Bootstrap, jQuery, TypeScript, Node/npm, bundlers, backends, databases, localStorage progress tracking.

---

## Folder structure

```text
lux-christi-blueprint/
├── index.html   ← page structure + CSS (<style>) + JS (<script>) in one file
└── README.md
```

Everything is kept in a single `index.html` so the site works when opened directly from disk or from any static host. If you prefer the split layout, cut the `<style>` block into `css/style.css` (and the `@media` rules into `css/responsive.css`) and the `<script>` block into `js/app.js`, then link them:

```html
<link rel="stylesheet" href="css/style.css">
<link rel="stylesheet" href="css/responsive.css">
<script src="js/app.js" defer></script>
```

---

## How to run

Open `index.html` in any modern browser. No install, no build step, no server required.

---

## How the HTML is structured

`index.html` contains, in order:

1. `<header>` — brand, primary `<nav>`, theme toggle, mobile menu button
2. `#overview` — hero, blueprint formula, the overall journey list
3. `#roadmap` — search box, level filters, expand/collapse, and the 20 learning stages (rendered by JS as `<details>` elements)
4. `#lab` — the 15 Lux Christi development milestones
5. `#technology` — technology progression flow (solid = used here, dashed gold = future Lux Christi tech)
6. `#connections` — Feature → Technology reference table
7. `#documents` — engineering documentation roadmap
8. `#philosophy` — four learning principles
9. `#mindset` — professional engineer mindset areas
10. `<footer>`

Each major section is a `<section>` with an `id` used by the navigation and scroll-spy.

---

## How the CSS is organised

The `<style>` block is split into numbered sections:

1. **Design tokens** — colour palette (navy, blue, white, charcoal, gold) as CSS variables on `:root`; `[data-theme="light"]` overrides the semantic tokens for the light theme.
2. **Base/reset** — typography, focus styles, skip link, `.container`, `.section`.
3. **Header & navigation**
4. **Hero** (incl. the journey list)
5. **Roadmap** — toolbar, stage cards, badges
6. **Project Lab** milestones
7. **Technology flow**
8. **Tables**
9. **Documentation groups**
10. **Philosophy & mindset**
11. **Footer / back-to-top**
12. **Responsive** — media queries at 1024px, 880px (mobile nav) and 600px

Layout is mobile-first in intent: grids collapse to single columns on small screens.

---

## How the JavaScript works

The `<script>` block has two halves:

**Content data** — plain arrays/objects:

- `STAGES` — the 20 learning stages (`title`, `level`, `learn`, `why`, `practice`, `lux`, `used`, optional `future`)
- `MILESTONES` — the 15 project-lab milestones
- `TECH` — technology progression (`now: true` = used in this site, `future: true` = future Lux Christi tech)
- `FEATURES` — feature → technology table rows
- `DOCS` — documentation roadmap groups
- `MINDSET` — mindset areas

**Render + interactions:**

- `render*()` functions build HTML from the data once on load
- `initTheme()` — dark/light toggle (respects OS preference; not persisted by design)
- `initNav()` — mobile navigation open/close, Escape to close
- `initScrollSpy()` — highlights the active nav link using `IntersectionObserver`
- `initRoadmapControls()` — search, level filter chips, expand/collapse all
- `initBackTop()` — back-to-top button

There is no state persistence, no storage and no network requests.

---

## How to edit the roadmap

Open `index.html`, find `const STAGES = [` and edit the objects. To add a stage, copy one object and change its fields:

```js
{ n: 21, title: "New Stage", tagline: "One-line summary", level: "advanced", future: true,
  learn: ["Topic A", "Topic B"],
  why: "Why this matters.",
  practice: ["Something to build"],
  lux: "How it connects to Lux Christi.",
  used: ["Feature it powers"] }
```

`level` must be one of `beginner`, `intermediate`, `advanced`, `professional` (it drives the badge and filter). Milestones, technologies, the feature table and documents are edited the same way in their respective arrays.

---

## How to deploy as a static website

Any static host works — upload the files as-is:

- **GitHub Pages**: push to a repository → Settings → Pages → deploy from the branch root.
- **Netlify / Vercel / Cloudflare Pages**: drag-and-drop the folder or connect the repo; no build command, publish directory `/`.
- **Any web server**: copy the folder into the server's public directory.

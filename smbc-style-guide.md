# SMBC Learning & Development — Style Guide
`smbc.css` · Version 1.0 · June 2025

---

## Overview

`smbc.css` is the shared stylesheet for all SMBC Learning & Development programme pages. It encodes the visual identity used across the Data-Driven Decision Making programme and is designed to be reused for any subsequent course or workshop pages.

The aesthetic is **corporate Japanese minimalism**: deep navy dominates, gold provides hierarchy and warmth, generous whitespace creates authority. Serif type (Noto Serif) carries titles and display text; sans-serif (Noto Sans) carries body copy and UI labels.

---

## Fonts

Both fonts load from Google Fonts. Include this link in every page `<head>` — or `smbc.css` handles it via `@import`.

| Role | Family | Weights used |
|---|---|---|
| Display / headings | Noto Serif | 400, 600, 700, 700 italic |
| Body / UI | Noto Sans | 300, 400, 500, 600 |

**Usage rule:** Use `var(--font-serif)` for any heading, number, or display element. Use `var(--font-sans)` for everything else.

---

## Colour Tokens

All colours are defined as CSS custom properties on `:root`. Always reference tokens — never hardcode hex values in page-level CSS.

```css
/* Core palette */
--navy:         #0b1f3a   /* primary background, text on light */
--navy-deep:    #071429   /* topbar, footer, darkest surfaces */
--navy-mid:     #163359   /* mid-tone navy fills */
--navy-light:   #1f4278   /* hover states on dark surfaces */

--gold:         #b8902a   /* primary accent, borders, icons */
--gold-light:   #d4a843   /* active states, hover gold */
--gold-pale:    #f0d98a   /* hero italic text, very light gold */

--cream:        #f5f2ec   /* page background */
--warm-white:   #faf8f4   /* card highlight background */
--white:        #ffffff   /* card / modal backgrounds */

--slate:        #5a6a7e   /* body text, secondary text */
--slate-light:  #8899aa   /* meta labels, placeholder text */

--rule:         #ddd5c0   /* borders, dividers */
--rule-light:   #ede8de   /* subtle inner borders */
```

### Colour hierarchy in practice

- **Page background:** `--cream`
- **Cards / panels:** `--white` or `--warm-white`
- **Dark sections** (topbar, footer, hero, modal): `--navy-deep` or `--navy`
- **Primary accent** (borders, icons, active tabs): `--gold`
- **Body copy on light:** `--slate`
- **Body copy on dark:** `rgba(255,255,255,0.6)`

---

## Spacing Scale

```css
--space-xs:   4px
--space-sm:   8px
--space-md:   16px
--space-lg:   28px
--space-xl:   48px
--space-xxl:  80px
```

---

## Layout Tokens

```css
--max-width:      1100px   /* content column max width */
--sidebar-width:  280px    /* right sidebar width */
--page-pad:       48px     /* horizontal page padding (24px on mobile) */
```

The standard two-column page layout is `.page-layout` — a CSS grid of `1fr` + `--sidebar-width`. It collapses to a single column below 860px.

---

## Components

### Topbar

```html
<header class="topbar">
  <div class="topbar__brand">
    <svg class="topbar__mark">...</svg>
    <div class="topbar__text">
      <span class="topbar__name">SMBC Group</span>
      <span class="topbar__sub">Learning & Development · APAC</span>
    </div>
  </div>
  <nav class="topbar__nav">
    <a href="#" class="active">Section A</a>
    <a href="#">Section B</a>
  </nav>
</header>
```

Sticky at top. Height 56px. Add `class="active"` to the current nav link.

---

### Hero

```html
<section class="hero">
  <div class="hero__rule"></div>
  <div class="hero__inner">
    <div class="hero__eyebrow">
      <div class="hero__eyebrow-line"></div>
      <span class="label">Programme Name</span>
    </div>
    <h1 class="hero__title">Main Title<br><em>Subtitle in italic gold</em></h1>
    <p class="hero__desc">Short programme description.</p>
    <div class="hero__meta">
      <div class="hero__meta-item">
        <span class="hero__meta-label">Label</span>
        <span class="hero__meta-value">Value</span>
      </div>
    </div>
  </div>
</section>
```

Dark navy background with subtle grid texture. Gold vertical rule on the right edge. Use `<em>` inside `hero__title` for italic gold emphasis.

---

### Tab Bar

```html
<div class="tab-bar">
  <button class="tab-bar__btn active" onclick="...">Tab One</button>
  <button class="tab-bar__btn" onclick="...">Tab Two</button>
</div>
```

Always sits below the hero. Toggle `class="active"` via JS.

---

### Section Header (day/chapter divider)

```html
<div class="section-header">
  <span class="pill">Day 1</span>
  <span class="section-header__title">Understanding Data Analytics</span>
</div>
```

Dark strip between the tab bar and content area. Use `.pill` for the label, plain text for the title.

---

### Page Layout

```html
<div class="page-layout">
  <main><!-- cards, lists, content --></main>
  <aside class="sidebar"><!-- sidebar cards --></aside>
</div>
```

Two-column grid. Sidebar is sticky. Collapses to single column on mobile.

---

### Content Card (module / topic)

```html
<div class="card">
  <div class="card__header">
    <div class="card__num">01</div>
    <div class="card__meta">
      <div class="card__tag">Module 1 · Day 1</div>
      <div class="card__title">Card Title</div>
      <div class="card__topics">
        <div class="card__topic">Topic one</div>
        <div class="card__topic">Topic two</div>
      </div>
    </div>
  </div>
  <div class="card__footer">
    <a href="#" class="btn">Open Exercise</a>
    <span class="pill--outline">Badge text</span>
  </div>
</div>
```

Modifier classes:
- `.card--highlighted` — gold left border + warm-white background (use for exercise / featured modules)
- `.card--active` — same as highlighted

---

### Sidebar Card

```html
<div class="sidebar-card sidebar-card--gold">
  <div class="sidebar-card__head">
    <div class="sidebar-card__label">Section Label</div>
    <div class="sidebar-card__title">Card Title</div>
  </div>
  <div class="sidebar-card__body">
    <div class="sidebar-row">
      <span class="sidebar-row__label">Key</span>
      <span class="sidebar-row__val">Value</span>
    </div>
  </div>
</div>
```

Default top border: `--navy`. Use `.sidebar-card--gold` for gold top border.

---

### Objectives Grid

```html
<div class="objectives">
  <div class="objective">
    <div class="objective__marker">1</div>
    <p class="objective__text">Objective text here.</p>
  </div>
</div>
```

Auto-fills columns at min 300px each. Separated by `--rule` colour gaps. White background per cell.

---

### Buttons

```html
<!-- Default: dark navy -->
<a href="#" class="btn">Label</a>

<!-- Gold fill -->
<a href="#" class="btn btn--gold">Label</a>

<!-- Outline badge (non-interactive) -->
<span class="pill--outline">Badge text</span>
```

---

### Formula Box (dark callout)

```html
<div class="formula-box">
  <div class="formula-box__label">Label</div>
  <div class="formula-box__text">The structured statement or formula goes here.</div>
  <div class="formula-box__example">Optional example in muted italic.</div>
</div>
```

Navy background, gold left border. Use for frameworks, templates, or key statements.

---

### Info Box

```html
<div class="info-box">
  <div class="info-box__label">Note</div>
  <p>Supporting text here.</p>
</div>
```

White background, gold top border. Use for facilitator notes, asides, or callouts on light backgrounds.

---

### Modal

```html
<div class="modal-overlay" id="myModal">
  <div class="modal">
    <button class="modal__close" onclick="closeModal()">✕</button>
    <!-- content -->
  </div>
</div>
```

```js
function openModal()  { document.getElementById('myModal').classList.add('open'); document.body.style.overflow='hidden'; }
function closeModal() { document.getElementById('myModal').classList.remove('open'); document.body.style.overflow=''; }
// Close on overlay click:
document.getElementById('myModal').addEventListener('click', e => { if(e.target===e.currentTarget) closeModal(); });
// Close on Escape:
document.addEventListener('keydown', e => { if(e.key==='Escape') closeModal(); });
```

---

### Utility Classes

| Class | Use |
|---|---|
| `.label` | Gold uppercase micro-label |
| `.label--light` | White/translucent version (on dark backgrounds) |
| `.label--slate` | Slate version |
| `.pill` | Gold filled pill badge |
| `.pill--navy` | Navy filled pill badge |
| `.pill--outline` | Outline badge (non-interactive) |
| `.rule` | Horizontal divider |
| `.rule--gold` | Gold-tinted divider |
| `.fade-up` | Entry animation (staggered for first 5 children) |

---

### Animations

Add `.fade-up` to sibling elements (e.g. a list of cards) for a staggered reveal on load. The class handles `animation-delay` for up to 5 children automatically.

For tab-panel switching, retrigger animations manually:

```js
el.style.animation = 'none';
el.offsetHeight; // reflow
el.style.animation = '';
```

---

## Page Template

Minimum HTML structure for a new page:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Page Title — SMBC L&D</title>
  <link rel="stylesheet" href="smbc.css">
</head>
<body>

  <header class="topbar">...</header>

  <section class="hero">...</section>

  <div class="tab-bar">...</div>

  <!-- For each tab panel: -->
  <div id="panel-X" class="panel active">
    <div class="section-header">...</div>
    <div class="page-layout">
      <main>...</main>
      <aside class="sidebar">...</aside>
    </div>
  </div>

  <footer>
    <span class="footer__brand">SMBC Group · Learning & Development · APAC</span>
    <span class="footer__note">Confidential</span>
  </footer>

  <script>
    // Tab switching
    function showPanel(id) {
      document.querySelectorAll('.panel').forEach(p => p.classList.remove('active'));
      document.getElementById('panel-' + id).classList.add('active');
    }
  </script>
</body>
</html>
```

---

## Do / Don't

| Do | Don't |
|---|---|
| Use CSS token variables for all colours | Hardcode hex values in page CSS |
| Use `var(--font-serif)` for headings | Use Arial, Inter, or system fonts |
| Keep label text SHORT and ALL CAPS | Write long descriptive labels |
| Use `.card--highlighted` sparingly (1–2 per page) | Highlight every card |
| Use Noto Serif numbers in `.card__num` | Use sans-serif for display numerals |
| Write hero `<em>` text for the programme subtitle | Use `<em>` for general emphasis |

# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

A single-file static landing page for an investment strategy consultancy. Everything — HTML, CSS, and JavaScript — lives in `index.html`. There is no build step, no package manager, and no external dependencies beyond two Google Fonts loaded via CDN.

## Running the Site

Open `index.html` directly in a browser. No server is required.

For a local dev server (enables live reload):
```bash
npx serve .
# or
python -m http.server 8080
```

## Architecture of index.html

The file is divided into three embedded blocks in order:

### `<style>` — CSS
- **CSS custom properties** at `:root` define the entire colour palette (`--primary`, `--secondary`, `--accent`, `--background`, `--text`, `--light-bg`) and shared tokens (radius, shadows, fonts, max-width, nav height).
- **`.fade-in` + `.visible`** are the animation primitives. JavaScript adds `.visible` via `IntersectionObserver`; delay variants `.d1`–`.d6` stagger card entrances.
- **Responsive breakpoints**: mobile-first base → `min-width: 768px` (tablet) → `min-width: 1024px` (desktop). A `max-width: 767px` block handles mobile-only overrides (hamburger menu, nav drawer).
- Section backgrounds alternate between `var(--background)` and `.section-light` (`var(--light-bg)`) for visual rhythm; `stats-bar`, `lead-magnet`, `final-cta`, and `footer` use dark `var(--primary)` / near-black backgrounds.

### HTML — Page Sections (in order)
| ID / element | Purpose |
|---|---|
| `#navbar` | Fixed top nav; gains `.scrolled` class (dark bg + shadow) after 60 px scroll |
| `#hero` | Full-viewport, Unsplash background image with CSS overlay gradient |
| `#why-us` | 6-card benefits grid |
| `.stats-bar` | 4 KPI counters (dark band) |
| `#process` | 4-step timeline; desktop shows a connecting line via `::before` pseudo-element on `.process-grid` |
| `#testimonials` | 3 testimonial cards |
| `#lead-magnet` | CTA banner; "Download" button smooth-scrolls to `#enquiry` |
| `#enquiry` | Enquiry form — see Form section below |
| `#faq` | Accordion FAQ |
| `#final-cta` | Conversion banner; CTA scrolls to `#enquiry` |
| `footer` | Contact, social links, disclaimer |

### `<script>` — JavaScript
Five self-contained behaviours, all vanilla JS, no globals exported:

1. **Sticky navbar** — `scroll` event toggles `.scrolled` on `#navbar`.
2. **Mobile menu** — `#hamburger` toggles `.open` on `#navLinks`; any link click closes the drawer.
3. **Smooth scroll** — intercepts all `a[href^="#"]` clicks, offsets for navbar height.
4. **IntersectionObserver** — adds `.visible` to every `.fade-in` element once it enters the viewport; then unobserves.
5. **FAQ accordion** — clicking a `.faq-q` button closes all panels, then opens the clicked one by setting `max-height` to `scrollHeight`.
6. **Form** — client-side validation (name length, email regex, phone regex) with inline `.err-msg` display; AJAX POST to `https://formsubmit.co/ajax/ukesston@gmail.com` using `fetch`; shows `#successBox` or `#errorBox` on response.

## Form Integration

The enquiry form POSTs via `fetch` to FormSubmit's AJAX endpoint. Hidden fields (`_subject`, `_captcha`, `_template`) are appended to `FormData` in JavaScript rather than as `<input type="hidden">` elements, keeping the HTML form clean.

To change the recipient email, update the `fetch` URL in the script:
```js
fetch('https://formsubmit.co/ajax/YOUR-EMAIL@example.com', ...)
```

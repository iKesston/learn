# Investment Strategy Landing Page

A single-file static landing page for a CapitalEdge Advisors — an investment strategy consultancy.

**Live site:** https://ikesston.github.io/learn/

## Stack

- Pure HTML, CSS, and JavaScript — no build step, no dependencies
- Two Google Fonts loaded via CDN (Inter, Playfair Display)
- Form submissions via [FormSubmit](https://formsubmit.co/) AJAX endpoint

## Running Locally

Open `index.html` directly in a browser — no server required.

For live reload:

```bash
npx serve .
# or
python -m http.server 8080
```

## Page Sections

| Section | Description |
|---|---|
| Navbar | Fixed top nav with scroll-triggered dark background |
| Hero | Full-viewport background with overlay gradient |
| Why Us | 6-card benefits grid |
| Stats Bar | 4 animated KPI counters |
| Process | 4-step timeline |
| Testimonials | 3 client testimonial cards |
| Lead Magnet | CTA banner linking to enquiry form |
| Enquiry Form | Client-validated form with AJAX submission |
| FAQ | Accordion-style FAQ section |
| Final CTA | Conversion banner |
| Footer | Contact info, social links, disclaimer |

## Form Setup

The enquiry form POSTs to FormSubmit's AJAX endpoint. To change the recipient email, update the `fetch` URL in the `<script>` block of `index.html`:

```js
fetch('https://formsubmit.co/ajax/YOUR-EMAIL@example.com', ...)
```

## Deployment

Pushing to `main` automatically triggers the GitHub Actions workflow at `.github/workflows/pages.yml`, which deploys the site to GitHub Pages. The live URL is available within ~1–2 minutes of a successful run.

## Project Structure

```
index.html   ← entire site (HTML + embedded CSS + embedded JS)
```

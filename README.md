# Lumière Bridal — Wedding Photography Booking Site

A single-page bridal photography booking website. No build step, no framework — everything (HTML, CSS, JavaScript) lives in one file: `index.html`.

## Features

- **Hero** — Full-viewport intro with CTA
- **About** — Photographer bio with two-column layout
- **Packages** — Three tiers (Elopement · Classic · Luxury) with pre-selection into the booking form
- **Gallery** — Responsive masonry-style photo grid
- **Booking Form** — 9-field form that submits via AJAX to [FormSubmit.co](https://formsubmit.co) — no page reload, spinner on submit, success/error states
- **Contact** — Phone, email, and Instagram cards

## Running Locally

```bash
python3 -m http.server 8080 --directory .
# open http://localhost:8080
```

## Tech Stack

| Concern | Solution |
|---|---|
| Fonts | Google Fonts — *Great Vibes* (display) + *Cormorant Garamond* (body) |
| Images | Unsplash (no account required) |
| Form backend | FormSubmit.co AJAX endpoint |
| Styling | Hand-written CSS with custom properties, no framework |
| Scripting | Vanilla JS — no libraries |

## Design Tokens

| Token | Value |
|---|---|
| Blush | `#f2a7b0` |
| Gold | `#c9a96e` |
| Rose | `#c9616d` |
| Background | `#fff8f5` |
| Text | `#3a2e2e` |

## Form Setup

Submissions go to FormSubmit.co. The first submission triggers a one-time confirmation email to the recipient address — approve it to activate the form.

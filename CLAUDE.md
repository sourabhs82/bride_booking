# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

A single-file static bridal photography booking website. Everything — HTML, CSS, and JavaScript — lives in one file: `index.html`. There is no build step, no package manager, and no framework.

## Running the Site

Open directly in a browser — no server required:

```bash
open index.html          # macOS
xdg-open index.html      # Linux
start index.html         # Windows
```

For live-reload during development (always use port 8080):

```bash
python3 -m http.server 8080 --directory /Users/siriusblack/Documents/bride-booking
# then open http://localhost:8080
```

## Architecture

All code is inline in `index.html` in this order:

1. **`<style>` block** — all CSS using custom properties defined at `:root`. Mobile-first with a single breakpoint at `768px`. No external CSS framework.
2. **HTML sections** (top → bottom): `nav`, `#hero`, `#about`, `#packages`, `#gallery`, `#booking`, `#contact`, `footer`
3. **`<script>` block** at end of `<body>` — three responsibilities:
   - Nav scroll class toggle (`.scrolled`)
   - Package card → form pre-selection (`data-package` attribute on `.pkg-btn` buttons maps to `<select id="package">`)
   - Form submit: collects fields into a plain object, POSTs JSON to `https://formsubmit.co/ajax/sourabh.sharma@gmail.com`, swaps form for success card on `json.success === 'true'`

## Key Design Tokens

Defined as CSS custom properties on `:root`:

| Variable | Value | Role |
|---|---|---|
| `--blush` | `#f2a7b0` | Accents, borders |
| `--blush-light` | `#fde8ec` | Section backgrounds |
| `--gold` | `#c9a96e` | Primary accent, buttons, dividers |
| `--rose` | `#c9616d` | Headings, prices, interactive states |
| `--text` | `#3a2e2e` | Body copy |
| `--font-display` | `'Great Vibes'` | Script headlines (loaded from Google Fonts) |
| `--font-body` | `'Cormorant Garamond'` | All body text (loaded from Google Fonts) |

## Form Submission

The booking form POSTs to FormSubmit.co's AJAX endpoint. The recipient email (`sourabh.sharma@gmail.com`) is hardcoded in the `fetch` call inside the `<script>` block. FormSubmit.co requires a one-time email confirmation before the first submission goes through.

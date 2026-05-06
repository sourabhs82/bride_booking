Translate the Ananya bridal photography website into Indian languages. Generate standalone translated HTML files and add a language switcher to all pages.

**Arguments:** $ARGUMENTS

## Step 1 — Parse the target language(s)

Read the arguments and determine which language(s) to generate. Valid values (case-insensitive):

| Argument | Output file | `lang` attribute | Script |
|----------|------------|------------------|--------|
| `hindi` | `index-hi.html` | `hi` | Devanagari |
| `punjabi` | `index-pa.html` | `pa` | Gurmukhi |
| `sindhi` | `index-sd.html` | `sd` | Arabic (Nastaliq) |
| `marathi` | `index-mr.html` | `mr` | Devanagari |
| `bengali` | `index-bn.html` | `bn` | Bengali |
| `all` | all five files | — | — |

Multiple languages can be specified space-separated: e.g. `hindi bengali`.

If no argument is provided or it is invalid, list the available languages and ask the user to pick.

## Step 2 — Read the source file

Read `index.html` in its entirety. This is the English source. Do NOT modify it except to add the language switcher (Step 5).

## Step 3 — Generate translated file(s)

For each requested language, create a new file in the project root (e.g. `index-hi.html`). Each file is a **complete standalone copy** of `index.html` with the following modifications:

### 3a. Set `<html lang>` and direction

Change `<html lang="en">` to the appropriate code from the table above.

**Sindhi only:** also add `dir="rtl"` → `<html lang="sd" dir="rtl">`.

### 3b. Swap Google Fonts

Replace the existing Google Fonts `<link>` tag with fonts that support the target script:

| Language | Display Font (`--font-display`) | Heading Font (`--font-heading`) | Body Font (`--font-body`) |
|----------|------|------|------|
| Hindi | `'Yatra One', serif` | `'Noto Sans Devanagari', sans-serif` | `'Noto Sans Devanagari', sans-serif` |
| Marathi | `'Yatra One', serif` | `'Noto Sans Devanagari', sans-serif` | `'Noto Sans Devanagari', sans-serif` |
| Punjabi | `'Baloo Paaji 2', serif` | `'Noto Sans Gurmukhi', sans-serif` | `'Noto Sans Gurmukhi', sans-serif` |
| Bengali | `'Galada', cursive` | `'Noto Sans Bengali', sans-serif` | `'Noto Sans Bengali', sans-serif` |
| Sindhi | `'Noto Nastaliq Urdu', serif` | `'Noto Sans Arabic', sans-serif` | `'Noto Sans Arabic', sans-serif` |

Build the Google Fonts URL to load both the display and body fonts with appropriate weights (400, 500, 600, 700). Update the CSS custom properties `--font-display`, `--font-heading`, and `--font-body` accordingly.

### 3c. Sindhi RTL CSS overrides

For Sindhi only, add these CSS rules after the existing responsive media queries:

```css
/* RTL overrides for Sindhi */
html[dir="rtl"] { direction: rtl; }
html[dir="rtl"] .nav-links { flex-direction: row-reverse; }
html[dir="rtl"] .about-text { text-align: right; }
html[dir="rtl"] .hero-kicker { direction: rtl; }
html[dir="rtl"] .pkg-features li { flex-direction: row-reverse; text-align: right; }
html[dir="rtl"] .pkg-features li::before { order: 1; }
html[dir="rtl"] .form-field select {
  background-position: left 1rem center;
  padding-left: 2.5rem;
  padding-right: 1rem;
}
html[dir="rtl"] .form-field label { text-align: right; }
html[dir="rtl"] .lang-switcher { flex-direction: row-reverse; }
html[dir="rtl"] .hero-frame .tl { left: auto; right: 1.5rem; transform: scaleX(-1); }
html[dir="rtl"] .hero-frame .tr { right: auto; left: 1.5rem; transform: none; }
html[dir="rtl"] .hero-frame .bl { left: auto; right: 1.5rem; transform: scale(-1); }
html[dir="rtl"] .hero-frame .br { right: auto; left: 1.5rem; transform: scaleY(-1); }
```

### 3d. Translate all user-visible text

Translate every string listed below into the target language. Follow these rules:

**Translation quality rules:**
- Use a **formal but warm** register appropriate for a premium bridal photography brand
- Indian wedding terms (मेहंदी/Mehendi, संगीत/Sangeet, शादी/Shaadi, बारात/Baraat, विदाई/Vidaai, हल्दी/Haldi) should be written in the **target script** (not left in Latin)
- **DO NOT translate** proper nouns: "Ananya", "Priya Sharma", city names (Mumbai, Delhi, Udaipur)
- Keep prices in `₹` format with Indian numbering (₹85,000 / ₹1,75,000 / ₹3,25,000)
- Keep the dollar amounts but translate the labels ("USD", "per session", "per wedding")
- Use **culturally appropriate example names** in form placeholders for each language
- **DO NOT translate** form field `name` attributes, `id` attributes, `data-package` attribute values, or `<option value="">` attribute values — JavaScript depends on these
- **DO translate** `<option>` display text (the text the user sees in dropdowns)
- Translate image `alt` texts for accessibility

**Complete string inventory — translate every item below:**

#### `<title>` tag (line 6)
- `Ananya — Bridal Photography` → translate "Bridal Photography", keep "Ananya"

#### Nav links (lines 643-648)
- `Ananya` — DO NOT translate (brand name, logo)
- `About`
- `Packages`
- `Gallery`
- `Book Now`

#### Hero section (lines 685-688)
- kicker: `विवाह चित्रकला · Bridal Photography` — translate the full text into the target language (both the Hindi part and English part become one unified string in the target language)
- h1: `Your Shaadi. Eternally Beautiful.`
- tagline: `From Mehendi to Vidaai — every precious moment, preserved forever.`
- CTA button: `Reserve Your Date`

#### About section (lines 703-730)
- section label: `Meri Kahani`
- section title: `Capturing the Soul of Every Shaadi`
- paragraph 1: `Namaste — I am Priya, a wedding photographer with over a decade of experience capturing the magic of Indian weddings across Mumbai, Delhi, Udaipur, and beyond. I understand the grandeur, the rituals, and the deeply intimate moments that make each Indian wedding utterly unique.`
- paragraph 2: `From the intricate mehndi patterns on a bride's hands to the radiant joy of a baraat procession — I see the divine in every detail. My work blends cinematic storytelling with a deep reverence for our traditions, creating heirlooms your family will treasure for generations.`
- paragraph 3: `Based in Mumbai. Available across India and internationally for destination weddings.`
- signature: `Priya Sharma` — DO NOT translate

#### Packages section (lines 739-811)
- section label: `Our Collections`
- section title: `Choose Your Package`

**Package 1 — Mehendi card:**
- event label: `Pre-Wedding Ceremonies`
- name: `Mehendi` — transliterate into target script
- price secondary: `~ $1,000 USD · per session` — keep dollar amount, translate "USD" label and "per session"
- features:
  - `4 hours of coverage`
  - `Mehendi & Haldi ceremonies`
  - `120 professionally edited photos`
  - `Private online gallery`
  - `High-resolution digital files`
- button: `Book This Package`

**Package 2 — Sangeet card:**
- badge: `Most Popular`
- event label: `Sangeet + Wedding Day`
- name: `Sangeet` — transliterate into target script
- price secondary: `~ $2,100 USD · per wedding`
- features:
  - `8 hours of coverage`
  - `Sangeet night + wedding day`
  - `350 professionally edited photos`
  - `Pre-wedding shoot included`
  - `Printed keepsake album`
  - `Private online gallery`
- button: `Book This Package`

**Package 3 — Shaadi Royale card:**
- event label: `Complete Wedding Experience`
- name: `Shaadi Royale` — transliterate into target script
- price secondary: `~ $3,900 USD · per wedding`
- features:
  - `Full 3-day coverage`
  - `All ceremonies included`
  - `600+ professionally edited photos`
  - `2 photographers + videographer`
  - `Drone aerial shots`
  - `Luxury lay-flat heirloom album`
- button: `Book This Package`

#### Gallery section (lines 821-851)
- section label: `Portfolio`
- section title: `A Glimpse of Our Work`
- alt text 1: `Indian bride with elaborate makeup and jewellery`
- alt text 2: `Indian bride in red and gold sari`
- alt text 3: `Indian bride in green and gold lehenga`
- alt text 4: `Indian bride in red bridal outfit`
- alt text 5: `Indian bride in wedding sari`
- alt text 6: `Indian bride in red and white sari`

#### Booking form section (lines 860-942)
- section label: `Reserve Your Date`
- section title: `Book a Session`
- subtitle: `Share your details and we'll respond within 24 hours to confirm your special day.`
- Form labels:
  - `Full Name *`
  - `Email Address *`
  - `Phone Number *`
  - `Wedding Date *`
  - `Preferred Time *`
  - `Package *`
  - `Venue / City *`
  - `Expected Guests *`
  - `Message` + `(optional)` span
- Form placeholders:
  - `Ananya Sharma` → use a culturally appropriate name for the target language
  - `ananya@example.com` → use matching email
  - `+91 98765 43210` → keep as-is
  - `Taj Lake Palace, Udaipur` → keep as-is (proper noun)
  - `500` → keep as-is
  - `Tell us about your vision, specific ceremonies you'd like covered, or any special requests…`
- Select option display texts (keep `value` attributes unchanged):
  - `Select a package`
  - `Mehendi — ₹85,000` → transliterate Mehendi, keep price
  - `Sangeet — ₹1,75,000` → transliterate Sangeet, keep price
  - `Shaadi Royale — ₹3,25,000` → transliterate, keep price
- Submit button: `Send My Enquiry`
- Error message: `Something went wrong. Please try again or email us directly.`
- Success heading: `Shubh Mangal!` — translate into target language equivalent
- Success message: `Your enquiry has been received. We'll be in touch within 24 hours to confirm your booking.`

#### Contact section (lines 951-978)
- section label: `Sampark Karen`
- section title: `Let's Connect`
- card headings: `Phone`, `Email`, `Instagram`
- card content values (+91 number, email address, @handle) — DO NOT translate

#### Footer (lines 983-993)
- `Ananya` — DO NOT translate (brand)
- tagline: `अनन्य — Unparalleled Bridal Artistry` — translate the full tagline into the target language
- nav links: `About`, `Packages`, `Gallery`, `Book Now`, `Contact` (same translations as top nav)
- copyright: `© 2026 Ananya Bridal Photography. All rights reserved.` — translate "All rights reserved", keep "Ananya Bridal Photography" and year

#### JavaScript strings (lines 1037, 1061)
- `Sending…` (inside innerHTML on line 1037)
- `Send My Enquiry` (inside innerHTML on line 1061)

### 3e. Add language switcher

Add a language switcher `<div>` inside the `<nav>` element, after the `.nav-links` `<ul>`. Use this HTML structure:

```html
<div class="lang-switcher">
  <a href="index.html">EN</a>
  <a href="index-hi.html">हि</a>
  <a href="index-pa.html">ਪੰ</a>
  <a href="index-sd.html">سن</a>
  <a href="index-mr.html">मा</a>
  <a href="index-bn.html">বা</a>
</div>
```

Mark the current language link with `class="active"`. For example, in `index-hi.html` the Hindi link gets `class="active"`.

Add this CSS for the switcher inside the `<style>` block:

```css
.lang-switcher {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  margin-left: 1.5rem;
  padding-left: 1.5rem;
  border-left: 1px solid rgba(201,149,42,0.35);
}
.lang-switcher a {
  font-family: var(--font-heading);
  font-size: 0.62rem;
  letter-spacing: 0.08em;
  color: rgba(255,255,255,0.5);
  padding: 0.2rem 0.35rem;
  transition: color var(--transition);
}
.lang-switcher a:hover { color: var(--gold-light); }
.lang-switcher a.active {
  color: var(--gold-light);
  border-bottom: 1px solid var(--gold);
}
@media (max-width: 767px) {
  .lang-switcher {
    margin-left: 0.75rem;
    padding-left: 0.75rem;
    gap: 0.3rem;
  }
  .lang-switcher a { font-size: 0.55rem; }
}
```

**Important:** Only include links for files that actually exist. If the user is generating only Hindi, the switcher should only have EN and हि links. If generating `all`, include all 6 links.

## Step 4 — Update the English `index.html`

Add the same language switcher to the original `index.html`:
1. Add the `.lang-switcher` CSS to the `<style>` block
2. Add the `<div class="lang-switcher">` after the `.nav-links` `<ul>` in the `<nav>`
3. Mark EN as `class="active"`

This is the **only** modification to make to `index.html`.

## Step 5 — Verify with Playwright

Start the local dev server on port 8080 if not already running:
```
python3 -m http.server 8080 --directory /Users/siriusblack/Documents/bride-booking
```

For each generated file:
1. Navigate to `http://localhost:8080/index-{code}.html`
2. Take a screenshot
3. Check that Indic text renders correctly (no empty boxes/tofu characters)
4. Verify the language switcher is visible in the nav

Also verify `http://localhost:8080/index.html` shows the language switcher.

Report results to the user with screenshots.

## Step 6 — Summary

Print a table listing:
- Each generated file name
- Target language and script
- File size
- Whether Playwright verification passed

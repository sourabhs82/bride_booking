# Ananya — Bridal Photography

> Luxury Indian wedding photography — from Mehendi to Vidaai, every precious moment preserved forever.

![screenshot](docs/screenshot.png)

## Tech Stack

![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=for-the-badge&logo=html5&logoColor=white)
![CSS3](https://img.shields.io/badge/CSS3-1572B6?style=for-the-badge&logo=css3&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black)
![GitHub Pages](https://img.shields.io/badge/GitHub%20Pages-222222?style=for-the-badge&logo=github&logoColor=white)
![FormSubmit](https://img.shields.io/badge/FormSubmit.co-FF6B6B?style=for-the-badge)

## Live Site

🌐 [View Live Site](https://sourabhs82.github.io/bride_booking/)

## File Structure

```
bride_booking/
├── index.html          # Entire site — HTML, CSS, and JS in one file
├── index-hi.html       # Hindi (हिन्दी) translation
├── docs/
│   └── screenshot.png  # Site preview image
├── .claude/
│   └── commands/
│       └── translate-site.md  # Slash command to generate translations
├── .github/
│   └── workflows/
│       └── deploy.yml  # GitHub Actions → GitHub Pages
└── README.md
```

## About the Project

A single-page booking website for **Ananya Bridal Photography**, designed to appeal to affluent Indian wedding clients. The design uses a rich jewel-tone palette — deep maroon, warm saffron, and gold — with Cinzel Decorative and EB Garamond fonts to evoke traditional Indian luxury. Key features include Indian wedding ceremony packages (Mehendi, Sangeet, Shaadi Royale) with INR pricing, a six-image bridal gallery, and a booking form that POSTs directly to FormSubmit.co.

### Multi-Language Support

The site includes a Hindi (हिन्दी) translation with a language switcher in the nav bar. Additional languages (Punjabi, Sindhi, Marathi, Bengali) can be generated using the `/translate-site` Claude Code slash command.

## How to Use

### View locally

```bash
# Option 1 — open directly
open index.html

# Option 2 — live-reload server (recommended)
python3 -m http.server 8080 --directory .
# then open http://localhost:8080
```

### Customise

| What | Where in index.html |
|------|---------------------|
| Contact email | `fetch('https://formsubmit.co/ajax/<email>')` in `<script>` |
| Colour palette | CSS custom properties on `:root` |
| Packages & pricing | `#packages` section |
| Gallery images | `#gallery` section — replace `src` URLs |

### Deploy

Push to the `main` branch — GitHub Actions deploys to GitHub Pages automatically.

## License

MIT

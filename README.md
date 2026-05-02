# Fenlo AI Website

Static website for [Fenlo AI](https://fenloai.com) — an AI implementation service for small businesses.

## What We Do

We build working AI systems: automation pipelines, custom software, and AI agents. Fixed pricing, no surprises. We will tell you if you do not need us yet.

## Tech Stack

- Pure HTML/CSS/JS — no build system, no frameworks
- GitHub Pages for static hosting
- Google Tag Manager for analytics
- Formspree for contact form handling
- Cal.com for booking discovery calls

## Project Structure

```
/
├── index.html                 # Homepage
├── css/styles.css             # Global styles (dark/light theme)
├── favicon.png                # Site favicon
├── og-image.png               # Social sharing image
├── pages/
│   ├── services.html          # 3-tier services overview
│   ├── work.html              # Capabilities showcase (demo projects)
│   ├── blog.html              # Blog listing
│   ├── blog/                  # 8 blog posts
│   ├── contact.html           # Contact form + discovery call CTA
│   ├── book-discovery.html    # Cal.com booking embed
│   ├── apply-briefing.html    # Redirects to book-discovery
│   ├── services/              # 9 redirect pages (old URLs)
│   └── legal/                 # Privacy + Terms
├── marketing/                 # Cold outreach materials
│   ├── cold-email-sequence.html
│   ├── linkedin-templates.html
│   ├── sales-sheet.html
│   └── poster.html
├── blogposts/                 # Blog source templates
│   ├── CLAUDE_INSTRUCTIONS.md
│   └── blog-template.html
└── assets/                    # Logo SVGs
```

## Deployment

Push to `main` on GitHub. GitHub Pages auto-deploys. No build step.

```bash
git add .
git commit -m "Your message"
git push origin main
```

## Key Files

| File | Purpose |
|------|---------|
| `index.html` | Homepage with hero, tiers, trust signals |
| `pages/services.html` | 3-tier pricing: Automation ($1.5K+), Custom Software ($3K+), AI Agents ($5K+) |
| `pages/work.html` | Demo projects (no client case studies yet) |
| `pages/contact.html` | Formspree form + discovery call CTA |
| `css/styles.css` | All styles including dark/light theme |

## Brand

- **Colors:** Dark olive (#6b7c3f), warm gold (#b8a04a)
- **Fonts:** DM Sans (body), Instrument Serif (display)
- **Voice:** Honest, direct, no jargon, no emojis
- **Primary CTA:** Book a free discovery call

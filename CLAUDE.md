# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a static website for Fenlo AI, an AI consulting and implementation service for small-medium businesses. The site emphasizes honest assessment over sales, with a philosophy that "not every business needs AI yet."

**Live Site:** https://fenloai.com

## Architecture

### File Structure

```
/
├── index.html              # Homepage (primary entry point)
├── favicon.png             # Site favicon
├── og-image.png            # Social sharing image (1200x630)
├── css/
│   └── styles.css         # Global styles with dark/light theme support
├── pages/
│   ├── blog.html          # Blog listing page
│   ├── blog/              # 8 individual blog post HTML files
│   ├── services.html      # Services overview (3-tier structure)
│   ├── services/          # 9 redirect pages (service1-9.html → services.html)
│   ├── work.html          # Capabilities showcase (demo projects, no client work yet)
│   ├── contact.html       # Contact form (Formspree) + discovery call CTA
│   ├── book-discovery.html # Cal.com booking embed for discovery calls
│   ├── apply-briefing.html # Redirects to book-discovery.html
│   └── legal/             # Privacy and terms pages
├── marketing/             # Cold outreach materials
│   ├── cold-email-sequence.html  # Interactive email templates (4 industries)
│   ├── cold-email-sequence.md    # Markdown version
│   ├── linkedin-templates.html   # Interactive LinkedIn templates
│   ├── linkedin-templates.md     # Markdown version
│   ├── sales-sheet.html          # Print-ready A4 one-pager
│   └── poster.html               # 4-format social media posters
├── blogposts/             # Blog source content (templates + guidelines)
│   ├── CLAUDE_INSTRUCTIONS.md  # Blog writing guidelines (READ THIS for blog work)
│   ├── blog-template.html      # Template for new blog posts
│   └── [topic-folders]/        # Individual blog post drafts
└── assets/
    └── fenloai-*.svg      # Logo files (icon + full logo)
```

### Technology Stack

- **Pure HTML/CSS/JavaScript** - No build system, frameworks, or package.json
- **Static hosting** - GitHub Pages with custom domain (fenloai.com)
- **Google Tag Manager** (GTM-MBJVZS7Z) for analytics
- **Google Fonts** - DM Sans (body), Instrument Serif (display)
- **Formspree** - Contact form handling
- **Cal.com** - Discovery call booking embed

### Theme System

The site has a comprehensive light/dark theme system:

- CSS custom properties in `:root` and `[data-theme="light"]`
- Theme toggle in navigation with localStorage persistence
- Primary accent: Dark olive (#6b7c3f)
- Secondary accent: Warm gold (#b8a04a) for CTAs
- Background uses glassmorphism effects with subtle gradients

**Important:** Light theme is the PRIMARY design aesthetic. Content should feel "light, clean, and approachable" per the brand guidelines.

## Key Design Patterns

### Navigation Structure

All pages include:
- Fenlo AI logo SVG (inline in HTML)
- Nav links: Home, Services, Work, Blog, Contact
- Theme toggle button (sun/moon icons)
- Mobile hamburger menu
- Reading progress indicator (top bar)
- Skip-to-content link (accessibility)

Navigation is consistent across all pages with appropriate relative paths.

### Page Structure Template

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <!-- Google Tag Manager (required) -->
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta name="description" content="...">
    <title>Page Title | Fenlo AI</title>
    <link rel="canonical" href="https://fenloai.com/path">
    <!-- Favicon, fonts, Open Graph, Twitter Card, JSON-LD -->
    <link rel="stylesheet" href="../css/styles.css">
</head>
<body>
    <!-- Google Tag Manager noscript -->
    <!-- Reading Progress Indicator -->
    <nav class="navbar">...</nav>
    <div class="mobile-nav">...</div>
    <main id="main-content">
        <!-- Page content -->
    </main>
    <footer>
        <!-- Privacy, Terms, Email, Copyright -->
    </footer>
    <!-- Cookie consent banner -->
    <!-- Theme toggle, mobile menu, animations scripts -->
</body>
</html>
```

### Card Components

The site uses two main card types:
1. `.glass-card` - For content sections with glassmorphism effects
2. `.service-card` - For clickable service/article links with hover effects

Both have mousemove listeners for radial gradient hover effects using CSS custom properties `--mouse-x` and `--mouse-y`.

## Working with Blog Posts

**CRITICAL:** Read `/blogposts/CLAUDE_INSTRUCTIONS.md` before creating or editing blog posts. It contains:
- Company mission, services, and target audience
- Brand voice guidelines (conversational, pragmatic, transparent)
- SEO requirements
- HTML structure and required components
- Citation and research guidelines
- CTA templates and placement rules

### Blog Post Workflow

1. **Research** - Gather 8-12 credible sources with citations
2. **Plan** - Create outline with sections and visual components
3. **Write** - Follow brand voice (no jargon, plain English, honest perspective)
4. **Build HTML** - Copy from `blogposts/blog-template.html`
5. **Deploy** - Save to `/pages/blog/slug-name.html` and update `/pages/blog.html` listing

### Blog HTML Components

Available components (from template):
- Table of Contents with anchor links
- Key Insight boxes
- Callout/Warning boxes
- Statistics grids
- Checklists with numbered steps
- Comparison tables
- Flow diagrams
- Mid-article CTA sections
- References with tooltips
- Social share buttons
- Related articles grid

### Critical Blog Rules

- **Every post MUST end with a CTA** to book a discovery call
- Target 1,500-2,500 words (~8-13 min reading time)
- Include citations for all statistics
- Use olive/sage green color scheme (not cyan/purple from dark theme)
- Write for small business owners (skeptical, busy, non-technical)
- Focus on honest assessment - acknowledge when AI isn't the answer

## Services Architecture

The site offers **3 service tiers** on a single page (`/pages/services.html`):

1. **Automation Pipelines** (Tier 1) — From $1,500
   - n8n/Make workflows connecting apps
   - Eliminates manual data entry
   - Timeline: 1-2 weeks

2. **Custom Software** (Tier 2) — From $3,000
   - Internal tools, dashboards, client portals
   - Built with AI-assisted coding (Cursor, Claude Code)
   - Timeline: 2-4 weeks

3. **AI Agents** (Tier 3) — From $5,000
   - Autonomous decision-making systems
   - Customer service agents, document processors
   - Timeline: 3-6 weeks

**Old service pages** (`/pages/services/service1-9.html`) are redirect pages pointing to the main services overview.

## SEO & Metadata

Every page requires:
- Unique meta description (150-160 chars)
- Proper title with "| Fenlo AI" suffix
- Canonical URL
- Open Graph tags (og:title, og:description, og:image, og:url)
- Twitter Card tags
- JSON-LD structured data (Organization, WebSite, FAQPage, Blog, etc.)

**Important:** Use absolute paths for shared assets: `/favicon.png`, `/og-image.png`

Structured data appears in:
- Homepage: Organization + WebSite + FAQPage
- Blog listing: Blog + BreadcrumbList
- Blog posts: BlogPosting + Organization

## Common Development Tasks

### Adding a New Blog Post

1. Research and gather sources
2. Copy `/blogposts/blog-template.html` to new topic folder
3. Update all `[PLACEHOLDERS]` in template
4. Write content following CLAUDE_INSTRUCTIONS.md voice
5. Add citations with tooltip references
6. Include mid-article and final CTAs
7. Save to `/pages/blog/slug-name.html`
8. Update `/pages/blog.html` with new post card
9. Add to JSON-LD structured data in blog.html

### Updating Services

The main services page is `/pages/services.html`. When editing:
- Maintain the 3-tier structure
- Keep pricing transparent
- Focus CTAs on discovery call: https://fenloai.com/pages/book-discovery.html
- The 9 old service pages are redirects — do not edit their content

### Theme Changes

Theme variables are in `/css/styles.css`:
- Edit `:root` for dark theme defaults
- Edit `[data-theme="light"]` for light theme overrides
- Theme toggle JS at bottom of each HTML file
- System preference detection on first load

### Adding Pages

1. Copy existing page structure
2. Update navigation links (account for relative paths)
3. Add Google Tag Manager snippets
4. Include theme toggle + mobile menu scripts
5. Update footer
6. Add to sitemap if using one

## Marketing Materials

The `/marketing/` folder contains outreach assets:
- **cold-email-sequence** — 4-email sequences for 4 industries (professional services, e-commerce, healthcare, real estate)
- **linkedin-templates** — Connection requests, DMs, comment templates, content calendar
- **sales-sheet** — Print-ready A4 one-pager with 3 tiers
- **poster** — 4 social media formats (square, story, landscape, A4 flyer)

All materials emphasize honest positioning: no fake case studies, transparent about being new.

## Brand Voice Guidelines

**Do:**
- Speak directly ("you" and "your business")
- Use plain English
- Be honest about limitations
- Give actionable advice
- Ask rhetorical questions

**Don't:**
- Use buzzwords ("leverage," "synergy," "disrupt")
- Make grandiose claims
- Use emojis (unless explicitly requested)
- Talk down to readers
- Be pushy or use fear tactics

**Example phrases:**
- "Here's the honest truth..."
- "Before you invest in AI, ask yourself..."
- "This might not be the answer you expected, but..."
- "Let's break this down in plain terms..."

## Analytics & Tracking

- Google Tag Manager (GTM-MBJVZS7Z) in all pages
- Cookie consent banner with localStorage
- User can accept/decline analytics
- Consent key: `fenloai_cookie_consent`
- Theme preference key: `fenloai_theme`

## Performance Notes

- Fonts preloaded with `rel="preconnect"` and `crossorigin`
- Scroll-triggered animations using IntersectionObserver
- Lazy-loaded effects (parallax, counters)
- Mobile-optimized with hamburger menu
- No build process = fast deployments

## Important Constraints

1. **No Node.js/npm** - Pure HTML/CSS/JS only
2. **Static hosting** - No server-side processing
3. **Inline JavaScript** - All scripts embedded in HTML
4. **Relative paths** - Carefully manage `../` for nested pages
5. **Manual updates** - Blog listing page must be manually updated when adding posts
6. **No emojis** - Brand guideline (unless user explicitly requests)
7. **Never inject JavaScript inside GTM or JSON-LD blocks** - These must remain pure

## Contact & Business Info

- **Email:** contact@fenloai.com
- **Primary CTA:** Free discovery call at /pages/book-discovery.html
- **Secondary CTA:** Executive AI Briefing at /pages/apply-briefing.html (redirects to book-discovery)
- **Target audience:** Small-medium business owners/decision-makers
- **Value proposition:** Honest AI assessment - will say "no" when AI isn't right

## Deployment

This site is designed for GitHub Pages or similar static hosting. There is no build step - simply push HTML/CSS/JS files to production.

```bash
git add .
git commit -m "Description of changes"
git push origin main
```

GitHub Pages auto-deploys from the `main` branch.

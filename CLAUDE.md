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
├── css/
│   └── styles.css         # Global styles with dark/light theme support
├── pages/
│   ├── blog.html          # Blog listing page
│   ├── blog/              # Individual blog post HTML files
│   ├── services.html      # Services overview
│   ├── services/          # Individual service detail pages (service1-9.html)
│   ├── contact.html
│   ├── book-discovery.html
│   ├── apply-briefing.html
│   └── legal/             # Terms and privacy pages
├── blogposts/             # Blog source content (markdown + HTML)
│   ├── CLAUDE_INSTRUCTIONS.md  # Blog writing guidelines (READ THIS for blog work)
│   ├── blog-template.html      # Template for new blog posts
│   └── [topic-folders]/        # Individual blog posts
└── assets/
    └── fenloai-*.svg      # Logo files
```

### Technology Stack

- **Pure HTML/CSS/JavaScript** - No build system, frameworks, or package.json
- **Static hosting** - Designed for GitHub Pages or similar
- **Google Tag Manager** (GTM-MBJVZS7Z) for analytics
- **Google Fonts** - Outfit font family

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
- Nav links: Home, Services, Blog, Contact
- Theme toggle button (sun/moon icons)
- Mobile hamburger menu

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

The site offers 9 services split into individual pages:
1. Executive AI Briefing (Free)
2. Custom Solutions
3. Smart Chatbots & Virtual Assistants
4. Document Q&A System
5. Workflow Automation
6. AI Workforce & Autonomous Agents
7. Business Intelligence & Automated Reporting
8. Generative AI Solutions
9. AI Security & Governance

Each service page follows a consistent structure:
- Hero with service name
- Problem statement
- Solution explanation
- Benefits/features
- Pricing/timeline info
- CTA to book discovery call

## SEO & Metadata

Every page requires:
- Unique meta description (150-160 chars)
- Proper title with "| Fenlo AI" suffix
- Canonical URL
- Open Graph tags (og:title, og:description, og:image, og:url)
- Twitter Card tags
- JSON-LD structured data (Organization, WebSite, FAQPage, Blog, etc.)

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

Service pages are in `/pages/services/service[1-9].html`. When editing:
- Maintain consistent structure with other service pages
- Keep pricing transparent (if mentioned)
- Focus CTAs on discovery call: https://fenloai.com/book-discovery.html
- Update `/pages/services.html` overview if adding/removing services

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

## Contact & Business Info

- **Email:** contact@fenloai.com
- **Primary CTA:** Free discovery call at /book-discovery.html
- **Secondary CTA:** Executive AI Briefing at /apply-briefing.html
- **Target audience:** Small-medium business owners/decision-makers
- **Value proposition:** Honest AI assessment - will say "no" when AI isn't right

## Deployment

This site is designed for GitHub Pages or similar static hosting. There is no build step - simply push HTML/CSS/JS files to production.

A deployment workflow exists at `.agent/workflows/deploy_to_github_pages.md` if GitHub Pages deployment is configured.

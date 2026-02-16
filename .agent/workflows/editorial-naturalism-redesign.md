# Fenlo AI Visual Redesign Workflow
# Codename: "Editorial Naturalism"
# Created: 2026-02-16

---

## Overview

**Concept:** Transform Fenlo AI from a polished-but-generic glassmorphism template into an editorially distinctive, warm, credible AI consulting site that visually embodies the brand promise: "Not every business needs AI yet."

**Aesthetic Direction:** High-quality editorial publication (Bloomberg Businessweek) meets organic warmth (botanical garden). Serif headlines, warm cream backgrounds, olive/sage palette, asymmetric layouts, restrained animation.

**Technical Constraints:**
- Pure HTML/CSS/JS -- no build system, no frameworks
- Static hosting (GitHub Pages)
- Single CSS file (`css/styles.css`, currently ~2600 lines)
- 24 HTML files total
- Google Fonts for typography
- Must maintain dark/light theme system
- Must preserve all existing functionality (forms, cal.com embeds, GTM, cookie consent)

---

## File Inventory (24 files)

### Root
- `index.html` (homepage)

### CSS
- `css/styles.css` (single stylesheet)

### Pages (23 HTML files)
- `pages/services.html` (overview)
- `pages/services/service1.html` through `service9.html` (9 files)
- `pages/blog.html` (listing)
- `pages/blog/faq-bots-complete-guide.html`
- `pages/blog/document-qa-guide-sme-roi.html`
- `pages/blog/ai-agents-guide-sme.html`
- `pages/blog/context-engineering.html`
- `pages/blog/agents-vs-automation.html`
- `pages/blog/ai-roi-framework.html`
- `pages/blog/escaping-pilot-purgatory.html`
- `pages/blog/mcp-protocol-guide.html`
- `pages/contact.html`
- `pages/book-discovery.html`
- `pages/apply-briefing.html`
- `pages/legal/privacy.html`
- `pages/legal/terms.html`

---

## Design Tokens (Reference)

### Typography
```
Display:  'Instrument Serif', Georgia, serif     -- H1, H2, pull quotes, hero
Body:     'DM Sans', -apple-system, sans-serif    -- Everything else
```

### Color Palette
```css
/* Dark theme (root) */
--bg-primary:            #0d0f0a;       /* warmer dark base */
--bg-secondary:          #141a10;
--bg-tertiary:           #1e2a1a;
--accent-primary:        #5d6e34;       /* deeper olive */
--accent-primary-light:  #8fa355;       /* existing light olive */
--accent-primary-dark:   #3d4a22;
--accent-secondary:      #c4944a;       /* richer gold */
--accent-secondary-light:#dbb066;
--accent-highlight:      #c4704b;       /* terracotta pop */
--text-primary:          #f0ede6;       /* warm off-white */
--text-secondary:        #a8a28a;       /* warm gray */

/* Light theme */
--bg-primary:            #faf7f2;       /* warm cream */
--bg-secondary:          #f3efe7;       /* slightly darker cream */
--bg-tertiary:           #ebe6db;
--text-primary:          #1a2418;       /* forest dark */
--text-secondary:        #4a5240;
```

### Google Fonts Import
```html
<link href="https://fonts.googleapis.com/css2?family=DM+Sans:ital,wght@0,400;0,500;0,600;0,700;1,400&family=Instrument+Serif:ital@0;1&display=swap" rel="stylesheet">
```

---

## SESSION 1: Design Foundation + Shared Shell

### Branch
```
git checkout -b redesign/session-1-foundation
```

### Goal
Update the CSS design system and shared HTML shell (font imports, navbar, footer) across all 24 files. After this session, every page should render with the new fonts, colors, and background treatment.

### Task 1.1: Update Google Fonts Import (ALL 24 HTML files)

**Action:** In every HTML file, replace the Outfit font `<link>` tag.

**Find (in all HTML files):**
```html
<link href="https://fonts.googleapis.com/css2?family=Outfit:wght@300;400;500;600;700;800&display=swap" rel="stylesheet">
```

**Replace with:**
```html
<link href="https://fonts.googleapis.com/css2?family=DM+Sans:ital,wght@0,400;0,500;0,600;0,700;1,400&family=Instrument+Serif:ital@0;1&display=swap" rel="stylesheet">
```

**Files:** All 24 HTML files listed above.

**Verification:** Open any page -- DM Sans should load for body text, Instrument Serif for headings.

---

### Task 1.2: Update CSS Custom Properties

**File:** `css/styles.css`

**Action:** Replace the `:root` block (lines 10-89) with updated design tokens.

**Key changes:**
- `--font-family` becomes `'DM Sans', -apple-system, BlinkMacSystemFont, sans-serif`
- Add `--font-display: 'Instrument Serif', Georgia, serif`
- Update all color values per the Design Tokens section above
- Remove all legacy color aliases (`--accent-cyan`, `--accent-purple`, `--accent-blue`, `--accent-green`, `--accent-orange`, `--accent-pink`, `--accent-sky`, `--accent-violet`, `--accent-gold`)
- Keep `--accent-red: #c4704b` (repurpose as terracotta highlight)
- `--font-weight-light: 300` changes to `--font-weight-normal: 400` as the baseline

**Action:** Update `[data-theme="light"]` block (lines 92-115) with warm cream palette.

---

### Task 1.3: Update Typography Declarations

**File:** `css/styles.css`

**Action:** Update heading and body font declarations.

**Changes:**
```css
/* Headings get Instrument Serif */
h1, h2, h3, h4, h5, h6 {
    font-family: var(--font-display);
    font-weight: var(--font-weight-bold);
    line-height: 1.15;
    color: var(--text-primary);
}

h1 { font-size: clamp(2.75rem, 5.5vw, 5rem); letter-spacing: -1.5px; }
h2 { font-size: clamp(2rem, 4vw, 3.25rem); letter-spacing: -0.5px; }
h3 { font-size: clamp(1.25rem, 2vw, 1.5rem); font-family: var(--font-family); }

/* Body uses DM Sans */
body {
    font-family: var(--font-family);
    font-weight: var(--font-weight-normal);  /* 400, not 300 */
    line-height: 1.65;
}

/* Buttons and nav use DM Sans explicitly */
.btn { font-family: var(--font-family); }
.nav-links a { font-family: var(--font-family); }
```

**Note:** H3 and below use DM Sans (body font) because small serif text is harder to read.

---

### Task 1.4: Redesign Background System

**File:** `css/styles.css`

**Action:** Remove `.bg-grid`, redesign `.bg-glow`, add grain overlay.

**Remove entirely:**
```css
.bg-grid { ... }
[data-theme="light"] .bg-grid { ... }
```

**Update `.bg-glow`:**
```css
.bg-glow {
    position: fixed;
    top: 0;
    left: 0;
    width: 100vw;
    height: 100vh;
    z-index: -1;
    pointer-events: none;
    background:
        radial-gradient(ellipse at 15% 50%, rgba(93, 110, 52, 0.08), transparent 40%),
        radial-gradient(ellipse at 85% 30%, rgba(143, 163, 85, 0.06), transparent 35%),
        radial-gradient(ellipse at 50% 90%, rgba(196, 148, 74, 0.04), transparent 30%);
}
```

**Add grain overlay (after `.bg-glow`):**
```css
.bg-grain {
    position: fixed;
    top: 0;
    left: 0;
    width: 100vw;
    height: 100vh;
    z-index: 0;
    pointer-events: none;
    opacity: 0.03;
    background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='noise'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23noise)'/%3E%3C/svg%3E");
    background-repeat: repeat;
    background-size: 256px 256px;
}

[data-theme="light"] .bg-grain {
    opacity: 0.025;
}
```

**Action:** In ALL HTML files, replace:
```html
<div class="bg-glow"></div>
<div class="bg-grid"></div>
```
with:
```html
<div class="bg-glow"></div>
<div class="bg-grain"></div>
```

**Files:** All 24 HTML files (find-and-replace).

---

### Task 1.5: Update Navbar Styling

**File:** `css/styles.css`

**Changes:**
- Update `.navbar` background for warmer tone
- Nav links use DM Sans medium weight at 0.95rem (already set, just verify)
- Update light theme navbar background to match warm cream

No HTML structure change needed -- just CSS refinement.

---

### Task 1.6: Update Footer + Copyright Year

**Action:** In ALL 24 HTML files, update the footer copyright.

**Find:**
```html
<p>&copy; 2025 Fenlo AI. All rights reserved.</p>
```

**Replace with:**
```html
<p>&copy; 2026 Fenlo AI. All rights reserved.</p>
```

**Files:** All 24 HTML files.

---

### Task 1.7: Update Light Theme Card Styles

**File:** `css/styles.css`

**Action:** Update `[data-theme="light"]` overrides for `.glass-card`, `.navbar`, `footer` to use warm cream tones instead of cool whites.

```css
[data-theme="light"] .glass-card {
    background: rgba(255, 253, 247, 0.75);
    border-color: rgba(93, 110, 52, 0.15);
}

[data-theme="light"] .glass-card:hover {
    background: rgba(255, 253, 247, 0.9);
    border-color: rgba(93, 110, 52, 0.3);
}
```

---

### Task 1.8: Update Gradient Text Classes

**File:** `css/styles.css`

**Action:** Update `.gradient-text` and `.gradient-text-light` to use the new color values and ensure they work with Instrument Serif.

---

### Task 1.9: Clean Up Legacy Color References in HTML

**Action:** In ALL HTML files, find any usage of `var(--accent-cyan)` and replace with `var(--accent-primary)`.

**Affected files:** Primarily `index.html` (lines 321, 326, 331, 336, 393, 399, 405, 411).

---

### Session 1 Acceptance Criteria
- [ ] All 24 pages render with Instrument Serif headings + DM Sans body
- [ ] Light theme uses warm cream (#faf7f2) not cool white
- [ ] Grid background removed, grain overlay visible on all pages
- [ ] Copyright shows 2026 on all pages
- [ ] No `var(--accent-cyan)` or other legacy aliases remain in HTML
- [ ] No visual regressions on any page (layouts intact)
- [ ] Both light and dark themes working

### Commit
```
git add -A && git commit -m "Session 1: Design foundation -- new typography, color palette, grain texture"
```

---

## SESSION 2: Homepage Transformation

### Branch
```
git checkout -b redesign/session-2-homepage
```

### Goal
Redesign the homepage (`index.html`) with editorial typography, asymmetric layouts, pull quotes, and zero inline styles. This is the showcase page that proves the new design language.

### Task 2.1: Refactor Hero Section

**File:** `index.html`

**Action:** Replace the centered hero with an asymmetric split layout.

**New structure:**
```html
<section class="hero">
    <div class="hero-grid">
        <div class="hero-content">
            <h1>Still Doing Manually<br>What AI Could Handle?</h1>
            <p class="hero-description">
                Free 2-hour Executive AI Briefing. We'll tell you honestly
                if AI makes sense -- or if traditional automation is the better fit.
            </p>
            <div class="hero-cta">
                <a href="pages/apply-briefing.html" class="btn btn-primary">Get Your Free Briefing</a>
            </div>
            <div class="hero-trust">
                <span class="trust-item">
                    <svg>...</svg> No pitch, no pressure
                </span>
                <span class="trust-item">
                    <svg>...</svg> Limited to qualified businesses
                </span>
                <span class="trust-item">
                    <svg>...</svg> Booking 2-3 weeks out
                </span>
            </div>
        </div>
        <div class="hero-stats">
            <div class="stat-badge">
                <span class="stat-number">73%</span>
                <span class="stat-label">of SMBs tested AI automation in 2024</span>
            </div>
            <div class="stat-badge">
                <span class="stat-number">10+ hrs</span>
                <span class="stat-label">saved with AI weekly</span>
            </div>
            <div class="stat-badge">
                <span class="stat-number">2-3 wks</span>
                <span class="stat-label">to first AI pilot live</span>
            </div>
        </div>
    </div>
</section>
```

**New CSS classes needed:**
```css
.hero-grid { display: grid; grid-template-columns: 1.2fr 0.8fr; gap: 4rem; align-items: center; }
.hero-content { text-align: left; }
.hero-stats { display: flex; flex-direction: column; gap: 1.5rem; }
.stat-badge { background: var(--glass-bg); border: 1px solid var(--glass-border); border-radius: var(--radius-lg); padding: var(--space-lg); }
.stat-number { font-family: var(--font-display); font-size: 2.5rem; font-weight: 700; color: var(--accent-primary); display: block; }
.stat-label { color: var(--text-secondary); font-size: 0.85rem; }
.hero-trust { display: flex; flex-wrap: wrap; gap: 1.5rem; margin-top: 2rem; }
.trust-item { display: flex; align-items: center; gap: 0.5rem; color: var(--text-secondary); font-size: 0.85rem; }
```

**Mobile (768px):** `.hero-grid` becomes single column, stats stack below text.

**Key:** Zero inline `style=""` attributes. ALL styling via CSS classes.

---

### Task 2.2: Add Editorial Pull Quote Section

**File:** `index.html`

**Action:** Add a new section between the hero and "Honest Truth" that serves as a visual breather and brand statement.

```html
<section class="pull-quote-section">
    <div class="container">
        <blockquote class="editorial-quote">
            "Not every business needs AI. We'd rather say <em>'not yet'</em>
            than sell you something you don't need."
        </blockquote>
    </div>
</section>
```

**CSS:**
```css
.pull-quote-section {
    padding: var(--space-3xl) 0;
    border-top: 1px solid var(--glass-border);
    border-bottom: 1px solid var(--glass-border);
}

.editorial-quote {
    font-family: var(--font-display);
    font-style: italic;
    font-size: clamp(1.5rem, 3vw, 2.5rem);
    line-height: 1.4;
    color: var(--text-primary);
    max-width: 800px;
    margin: 0 auto;
    text-align: center;
    position: relative;
}

.editorial-quote em {
    color: var(--accent-primary);
    font-style: italic;
}
```

---

### Task 2.3: Refactor "Honest Truth" Section

**Action:** Move from centered layout to left-aligned header with right-aligned card stack.

**Keep existing glass-card pattern** but left-align the section header. Remove inline styles.

---

### Task 2.4: Redesign "How We Work" Section

**Action:** Replace 4 identical glass-cards with a horizontal stepper component.

```html
<section class="section">
    <div class="container">
        <h2 class="gradient-text">How We Work</h2>
        <div class="stepper">
            <div class="stepper-step">
                <span class="stepper-number">1</span>
                <div class="stepper-connector"></div>
                <h3>Free Assessment</h3>
                <p>We learn your business and where you're stuck.</p>
            </div>
            <!-- repeat for steps 2-4 -->
        </div>
    </div>
</section>
```

**CSS for stepper:**
```css
.stepper { display: flex; gap: 0; position: relative; }
.stepper-step { flex: 1; text-align: center; position: relative; padding: 0 var(--space-md); }
.stepper-number {
    display: inline-flex; align-items: center; justify-content: center;
    width: 48px; height: 48px;
    background: var(--accent-primary); color: #fff;
    border-radius: 50%; font-family: var(--font-display);
    font-size: 1.25rem; margin-bottom: var(--space-md);
}
.stepper-connector {
    position: absolute; top: 24px; left: calc(50% + 24px);
    width: calc(100% - 48px); height: 2px;
    background: var(--glass-border);
}
.stepper-step:last-child .stepper-connector { display: none; }
```

---

### Task 2.5: Refactor "What We Build" Service Grid

**Action:** Make Executive AI Briefing a featured (2-column wide) card, rest normal.

```css
.grid-featured .service-card:first-child {
    grid-column: span 2;
}
```

---

### Task 2.6: Redesign "Results" Section with Editorial Stats

**Action:** Make the statistics oversized editorial elements instead of small text inside a glass card.

```css
.editorial-stat {
    font-family: var(--font-display);
    font-size: clamp(3rem, 6vw, 5rem);
    font-weight: 700;
    color: var(--accent-primary);
    line-height: 1;
    letter-spacing: -2px;
}
```

---

### Task 2.7: Fix SVG Checkmark Icons

**Action:** Fix the hero trust signal SVG icons -- they have viewBox="0 0 24 24" content but width="16" height="16", causing clipping.

**Fix:** Either update the viewBox or use the correct 16x16 path data.

---

### Task 2.8: Eliminate ALL Inline Styles

**Action:** Audit every remaining `style=""` attribute in `index.html` and convert to CSS classes.

**Current inline style count:** ~30+ inline style declarations on homepage.
**Target:** Zero inline styles in body content (GTM noscript iframe is acceptable).

---

### Session 2 Acceptance Criteria
- [ ] Hero is asymmetric (text left, stats right)
- [ ] Pull quote section present and styled editorially
- [ ] "How We Work" uses stepper instead of 4 cards
- [ ] Zero inline `style=""` attributes in body content
- [ ] All sections have class-based styling
- [ ] Statistics rendered at editorial scale
- [ ] SVG icons render without clipping
- [ ] Mobile layout works (hero stacks vertically)
- [ ] Scroll animations functional

### Commit
```
git add -A && git commit -m "Session 2: Homepage editorial redesign -- asymmetric hero, pull quotes, stepper"
```

---

## SESSION 3: Services Pages (10 files)

### Branch
```
git checkout -b redesign/session-3-services
```

### Goal
Bring all 10 service pages into consistency with the new design system. Fix all bugs. Consolidate card types. Add missing components (breadcrumbs, badges, scripts).

### Task 3.1: Consistency Sweep -- All 9 Detail Pages

**Action (every service detail page, service1-9.html):**

1. **Add breadcrumbs** below page-header (before main content):
```html
<nav class="breadcrumbs" aria-label="Breadcrumb">
    <a href="../../index.html">Home</a>
    <span class="separator">/</span>
    <a href="../services.html">Services</a>
    <span class="separator">/</span>
    <span class="current">[Service Name]</span>
</nav>
```

2. **Add IntersectionObserver script** (same as homepage) to the `<script>` block at bottom of each page.

3. **Add card mousemove hover effect script** to each page that has `.glass-card` or `.service-card` elements.

4. **Move CTA section inside `<main>`** (fix Service 2 where it's outside).

5. **Add missing meta tags** (`meta name="keywords"`, `meta name="author"`, `meta name="robots"`) to services 1, 2, 4-9 (service 3 and overview already have them).

---

### Task 3.2: Add Missing Badges

**Files:** `service2.html`, `service3.html`

**Action:** Add `.badge` element to page-header:
- Service 2: `<div class="badge">Tailored to Your Business</div>`
- Service 3: `<div class="badge">Most Popular First Project</div>`

---

### Task 3.3: Fix Bugs

1. **Service 3 -- Invalid JSON-LD:** Remove trailing comma after `"areaServed": "Worldwide",`
2. **Service 6 -- Emoji violation:** Remove leaf emoji from chat demo (line 258)
3. **Service 2 -- CTA outside main:** Move `section.cta-section` inside `<main>`

---

### Task 3.4: Consolidate Card Types

**File:** `css/styles.css`

**Action:** Create unified card variants and deprecate page-specific card classes.

**New system (3 variants):**
```css
/* Base glass card -- already exists, keep as-is */
.glass-card { ... }

/* Numbered step card -- replaces .app-card, .help-item, .framework-card */
.glass-card--step {
    display: flex;
    align-items: flex-start;
    gap: var(--space-lg);
}
.glass-card--step .step-indicator {
    background: rgba(93, 110, 52, 0.15);
    color: var(--accent-primary-light);
    padding: var(--space-sm);
    border-radius: 50%;
    font-weight: var(--font-weight-bold);
    min-width: 45px;
    text-align: center;
    font-family: var(--font-display);
}

/* Accent-top card -- replaces .pillar-card, .feature-card.with-bar */
.glass-card--accent {
    border-top: 4px solid var(--accent-primary);
}
.glass-card--accent:hover {
    border-top-color: var(--accent-primary-light);
}
```

**HTML updates needed:** Update card classes in service2 (.scope-card), service3 (.value-card stays but icons made consistent), service4 (.value-card), service5 (.app-card), service6 (.feature-card.with-bar), service7 (.metric-card), service9 (.pillar-card, .framework-card).

**Note:** Keep existing CSS for deprecated card classes during transition (can remove in Session 5 cleanup). Just update HTML to use new classes.

---

### Task 3.5: Refactor Inline Styles

**Priority files (most inline styles):**

1. **Service 7** (~12 inline declarations): Create CSS classes for the conversational mockup:
   - `.chat-mockup`
   - `.chat-mockup-query`
   - `.chat-mockup-response`
   - `.chat-mockup-meta`

2. **Service 9** (~10 inline declarations): Create CSS class for the inline grid layout and framework card header styling.

3. **All service pages:** Convert `style="color: var(--text-secondary);"` and `style="font-size: ..."` to utility classes (these already exist: `.text-muted`, `.text-sm`, etc.).

---

### Task 3.6: Services Overview Page

**File:** `pages/services.html`

**Action:**
- Apply editorial serif to page heading
- Update filter button styling for new palette
- Verify card grid works with new card styles

---

### Session 3 Acceptance Criteria
- [ ] All 9 detail pages have breadcrumbs
- [ ] All 9 detail pages have IntersectionObserver + mousemove scripts
- [ ] Services 2 and 3 have badges
- [ ] JSON-LD validates on all service pages (no trailing commas)
- [ ] No emoji in Service 6
- [ ] Service 2 CTA inside `<main>`
- [ ] Card types reduced to 3 unified variants (HTML updated)
- [ ] Inline styles reduced by 80%+ across service pages
- [ ] All meta tags consistent

### Commit
```
git add -A && git commit -m "Session 3: Services consistency -- breadcrumbs, card consolidation, bug fixes"
```

---

## SESSION 4: Blog, Contact, Booking Pages

### Branch
```
git checkout -b redesign/session-4-remaining-pages
```

### Goal
Apply the new design system to blog listing, contact, booking pages, and legal pages. Move inline styles to CSS.

### Task 4.1: Blog Listing Page

**File:** `pages/blog.html`

**Action:**
- Apply editorial serif to page heading
- Consider featuring first/latest post larger than others (optional enhancement)
- Verify card styling consistent with new system
- Breadcrumbs already present -- verify styling

---

### Task 4.2: Blog Post Pages (8 files)

**Files:** All 8 blog post HTML files in `pages/blog/`

**Action:**
- Verify font import updated (should be done in Session 1)
- Verify copyright year updated
- Verify blog post headings render in Instrument Serif
- Check that blog-specific components (TOC, callout boxes, citation tooltips) work with new palette
- Ensure footer and nav consistent

**Note:** Blog posts have extensive internal styling. Only update shared components (nav, footer, fonts). Do not restructure blog post content layouts.

---

### Task 4.3: Contact Page

**File:** `pages/contact.html`

**Action:**
- Add breadcrumbs
- Verify engagement cards styled correctly with new system
- Update form field styling for warmer palette (border colors, focus states)
- Verify form validation colors work with new accent palette

---

### Task 4.4: Booking Pages

**Files:** `pages/book-discovery.html`, `pages/apply-briefing.html`

**Action:**
- Add breadcrumbs
- Move inline `<style>` blocks to `css/styles.css` (the `.cal-embed-container` styles)
- Standardize embed dimensions (decide on one size or document why they differ)
- Verify Cal.com embed renders correctly with new background color

---

### Task 4.5: Legal Pages

**Files:** `pages/legal/privacy.html`, `pages/legal/terms.html`

**Action:**
- Verify font import updated
- Verify copyright year
- Verify legal content renders readably with new body font

---

### Session 4 Acceptance Criteria
- [ ] Blog listing styled with new design system
- [ ] All 8 blog posts render correctly with new fonts
- [ ] Contact page has breadcrumbs, updated form styling
- [ ] Booking pages have no inline `<style>` blocks
- [ ] Legal pages render correctly
- [ ] All pages have consistent nav/footer

### Commit
```
git add -A && git commit -m "Session 4: Blog, contact, booking pages aligned to new design system"
```

---

## SESSION 5: Animation, Polish & QA

### Branch
```
git checkout -b redesign/session-5-polish
```

### Goal
Implement consistent animation system, remove deprecated CSS, performance audit, final QA across all pages and both themes.

### Task 5.1: Unified Animation System

**File:** `css/styles.css`

**Action:** Implement consistent page-load and scroll-reveal animations.

**Page-load sequence (applied via CSS, no JS needed):**
```css
.navbar { animation: fadeIn 0.3s ease-out; }
.page-header, .hero { animation: fadeIn 0.5s ease-out 0.1s both; }
.section:first-of-type { animation: fadeIn 0.5s ease-out 0.3s both; }
```

**Scroll reveals (standardize across all pages):**
- Ensure IntersectionObserver script is present on ALL pages
- Refine animation: gentle fade (remove translateY bounce for more editorial feel):
```css
.animate-on-scroll {
    opacity: 0;
    transition: opacity 0.8s ease-out;
}
.animate-on-scroll.visible {
    opacity: 1;
}
```

**Counter animation:** Ensure it works on homepage statistics.

---

### Task 5.2: Hover State Refinement

**Action:** Audit and refine all hover states for new aesthetic.

**Card hover -- more subtle:**
```css
.glass-card:hover {
    transform: translateY(-3px);  /* reduced from -5px */
    border-color: var(--glass-border-hover);
    box-shadow: var(--shadow-md);
}
```

**Button hover -- warmer glow:**
```css
.btn-primary:hover {
    transform: translateY(-2px);
    box-shadow: 0 8px 25px rgba(93, 110, 52, 0.35);
}
```

---

### Task 5.3: CSS Cleanup

**File:** `css/styles.css`

**Action:**
1. Remove deprecated card class definitions that are no longer referenced in HTML:
   - `.scope-card` (if all replaced)
   - `.app-card`, `.app-grid`, `.app-number` (if all replaced)
   - `.capability-card` (appears unused)
   - `.option-card` (appears unused)
2. Remove legacy color alias declarations
3. Remove `.bg-grid` and `[data-theme="light"] .bg-grid` rules
4. Organize CSS into clear sections with comments
5. Verify no orphaned selectors

---

### Task 5.4: Performance Check

**Action:**
1. Verify `<link rel="preconnect">` for Google Fonts is present on all pages
2. Ensure `display=swap` on font import (prevents FOIT)
3. Check that `.bg-grain` SVG filter doesn't cause paint performance issues
4. Verify `prefers-reduced-motion` media query still properly disables animations
5. Ensure backdrop-filter doesn't cause lag on mobile Safari

---

### Task 5.5: Cross-Page QA Checklist

**Action:** Verify each of the following on ALL 24 pages:

| Check | Status |
|-------|--------|
| Instrument Serif renders on H1/H2 | |
| DM Sans renders on body/nav/buttons | |
| Light theme: warm cream background (#faf7f2) | |
| Dark theme: warm dark background (#0d0f0a) | |
| Grain overlay visible (subtle) | |
| No grid background visible | |
| Copyright says 2026 | |
| No inline `style=""` on content elements | |
| No `var(--accent-cyan)` in HTML | |
| Breadcrumbs present (where applicable) | |
| Scroll animations trigger correctly | |
| Card hover effects work | |
| CTA buttons styled correctly | |
| Mobile nav works (768px breakpoint) | |
| Footer links work | |
| Theme toggle works | |
| Cookie consent works | |

---

### Task 5.6: Contrast Ratio Audit

**Action:** Verify WCAG AA contrast ratios with new palette:
- `#1a2418` on `#faf7f2` (light theme text on background) -- should pass
- `#f0ede6` on `#0d0f0a` (dark theme text on background) -- should pass
- `#5d6e34` on `#faf7f2` (accent on light bg) -- check, may need adjustment
- Button text (`#fff`) on `#5d6e34` button -- check contrast

If any fail, adjust the specific color value to pass.

---

### Session 5 Acceptance Criteria
- [ ] Consistent animation behavior across all 24 pages
- [ ] No janky hover effects or layout shifts
- [ ] Both themes polished and complete
- [ ] CSS file is cleaner (deprecated classes removed)
- [ ] All pages pass basic accessibility contrast checks
- [ ] Performance acceptable on mobile
- [ ] `prefers-reduced-motion` still works
- [ ] No console errors on any page

### Commit
```
git add -A && git commit -m "Session 5: Animation polish, CSS cleanup, QA pass"
```

---

## Merge Strategy

After all 5 sessions are complete and verified:

```
git checkout main
git merge redesign/session-1-foundation
git merge redesign/session-2-homepage
git merge redesign/session-3-services
git merge redesign/session-4-remaining-pages
git merge redesign/session-5-polish
```

Alternatively, if working sequentially on main:
```
# Each session commits directly to a single redesign branch
git checkout -b redesign/editorial-naturalism
# ... complete all 5 sessions with individual commits ...
git checkout main
git merge redesign/editorial-naturalism
```

---

## Risk Register

| Risk | Mitigation |
|------|-----------|
| Font loading causes layout shift | Use `display=swap` + preconnect. Test on slow connections. |
| Warm cream looks "yellow" on some displays | Test on multiple screens. Keep saturation subtle. |
| Serif font feels "old-fashioned" to tech audience | Instrument Serif is modern and sharp -- not classical. Pair with DM Sans for balance. |
| Card consolidation breaks a page | Keep deprecated CSS classes during transition. Only remove in Session 5 after QA. |
| CSS cascade changes break unexpected pages | Session 1 changes cascade everywhere -- test ALL pages after Session 1. |
| Grain overlay causes GPU performance issues | Use low opacity (3%). Test on mobile. Disable if needed with `prefers-reduced-motion`. |
| Blog posts have internal styles that conflict | Blog posts use components from styles.css -- verify they still work after color/font changes. |

---

## Timeline Estimate

| Session | Scope | Estimated Effort |
|---------|-------|-----------------|
| Session 1 | Foundation + Shell (24 files) | 1-2 hours |
| Session 2 | Homepage (1 file, heavy) | 1-2 hours |
| Session 3 | Services (10 files) | 2-3 hours |
| Session 4 | Blog/Contact/Booking (13 files) | 1-2 hours |
| Session 5 | Polish + QA (all files) | 1-2 hours |
| **Total** | | **6-11 hours** |

---

## Quick Reference: Key Decisions

1. **Why Instrument Serif?** -- Editorial authority without being stuffy. New enough to feel fresh. Pairs well with geometric sans-serif.
2. **Why DM Sans over Outfit?** -- Warmer geometric feel, better readability at body sizes, not becoming the "AI site default" like Outfit.
3. **Why warm cream not white?** -- Signals "trusted publication" over "SaaS product." Olive green pops better on cream than on pure white.
4. **Why remove the grid background?** -- It reads as "tech company template." The grain texture is more organic and matches the natural brand identity.
5. **Why asymmetric hero?** -- Centered layouts are the #1 predictor of "template site." Left-aligned text with right visual creates editorial flow and visual tension.

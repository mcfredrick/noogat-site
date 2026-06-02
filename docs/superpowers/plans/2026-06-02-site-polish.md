# Noogat Site Polish Pass — Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Polish the Noogat marketing site with a dark hero redesign, OG share image, scroll animations, and visual depth improvements across all sections.

**Architecture:** Pure HTML/CSS/JS — no build step, no framework. All changes are in `/Users/matt/Code/noogat-site/index.html` plus a new `assets/og-image-source.html` and generated `assets/og-image.png`. The site uses `_shared.css` for brand tokens; never use raw hex values in new CSS — always reference the CSS custom properties defined there or in the existing `<style>` block.

**Tech Stack:** HTML5, CSS3 (custom properties, flexbox, grid, CSS transitions), vanilla JS (IntersectionObserver for scroll animations), headless Chrome for OG image PNG generation.

**Design decisions locked in:**
- Hero: dark purple gradient background (`#0f0020 → #1a0040 → #25003a`), radial glow orbs, tilted phone screenshot, gradient band with Siri quote, app-style stat tiles with emoji icons
- OG image: 1200×630 landscape, same dark aesthetic — logo + NOOGAT wordmark lockup, tagline, stat tiles, tilted phone screenshot, gradient band at bottom
- Polish directions: visual depth (shadows, glassmorphism), layout dynamism (tilted elements, overlaps), scroll animations (fade-up on entry)
- Mobile-first: primary audience is iPhone users

---

## File Map

| File | Change |
|---|---|
| `index.html` | Hero CSS + HTML rewrite; scroll animation CSS + JS; section polish CSS |
| `assets/og-image-source.html` | New — 1200×630 OG image HTML source |
| `assets/og-image.png` | New — generated from og-image-source.html via headless Chrome |

---

### Task 1: OG Image — source file

**Files:**
- Create: `assets/og-image-source.html`

The source file renders at exactly 1200×630 CSS pixels with no scrollbars. Assets are referenced relative to the `assets/` directory so headless Chrome can load them via `file://`.

- [ ] **Step 1: Create `assets/og-image-source.html`**

```html
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<style>
* { box-sizing: border-box; margin: 0; padding: 0; }
html, body { width: 1200px; height: 630px; overflow: hidden; }
body {
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif;
  background: linear-gradient(135deg, #0f0020 0%, #1a0040 50%, #250040 100%);
  display: flex;
  align-items: stretch;
  position: relative;
  overflow: hidden;
}
.glow-purple {
  position: absolute; top: -150px; right: 240px;
  width: 520px; height: 520px;
  background: radial-gradient(circle, rgba(124,34,217,0.5) 0%, transparent 65%);
  pointer-events: none;
}
.glow-pink {
  position: absolute; bottom: -80px; left: 60px;
  width: 360px; height: 360px;
  background: radial-gradient(circle, rgba(201,27,91,0.28) 0%, transparent 65%);
  pointer-events: none;
}
.og-left {
  flex: 1;
  padding: 52px 32px 104px 56px;
  display: flex;
  align-items: flex-start;
  justify-content: center;
  position: relative; z-index: 1;
}
.og-content { display: flex; flex-direction: column; gap: 32px; }
.og-lockup { display: flex; flex-direction: row; align-items: flex-start; gap: 28px; }
.og-logo { width: 188px; height: 188px; object-fit: contain; object-position: left top; flex-shrink: 0; }
.og-copy { display: flex; flex-direction: column; gap: 14px; }
.og-wordmark {
  font-size: 110px; font-weight: 900; letter-spacing: -0.05em; line-height: 0.92;
  background: linear-gradient(135deg, #bf5fff 0%, #ff5c8d 55%, #a3e635 100%);
  -webkit-background-clip: text; -webkit-text-fill-color: transparent;
}
.og-tagline { font-size: 26px; color: rgba(255,255,255,0.6); line-height: 1.4; }
.og-tagline strong { color: rgba(255,255,255,0.92); font-weight: 600; }
.og-stats { display: flex; gap: 10px; }
.og-stat {
  flex: 1;
  background: rgba(255,255,255,0.06);
  border: 1px solid rgba(255,255,255,0.13);
  border-radius: 14px;
  padding: 18px 20px 16px;
  display: flex; flex-direction: column;
  min-height: 170px;
}
.og-stat .slabel { font-size: 12px; font-weight: 700; letter-spacing: 0.08em; text-transform: uppercase; color: rgba(255,255,255,0.35); }
.og-stat .sval { font-size: 34px; font-weight: 800; letter-spacing: -0.02em; line-height: 1; margin-top: 6px; }
.og-stat.purple .sval { color: #bf5fff; }
.og-stat.green  .sval { color: #a3e635; }
.og-stat.pink   .sval { color: #ff5c8d; }
.og-stat .sicon { margin-top: auto; padding-top: 12px; font-size: 52px; line-height: 1; opacity: 0.75; }
.og-right {
  width: 360px; flex-shrink: 0;
  display: flex; align-items: flex-end; justify-content: center;
  padding: 0 24px 52px 0;
  position: relative; z-index: 1; overflow: hidden;
}
.og-phone {
  width: 260px; height: 560px;
  border-radius: 32px; object-fit: cover; object-position: top center;
  transform: rotate(2deg) translateY(52px);
  box-shadow: 0 28px 80px rgba(0,0,0,0.65), 0 0 0 1.5px rgba(255,255,255,0.12);
  display: block;
}
.og-band {
  position: absolute; bottom: 0; left: 0; right: 0; height: 52px;
  background: linear-gradient(90deg, #7C22D9, #C91B5B);
  display: flex; align-items: center; padding: 0 56px; z-index: 3;
}
.og-band span { font-size: 18px; font-style: italic; font-weight: 500; color: rgba(255,255,255,0.92); }
</style>
</head>
<body>
  <div class="glow-purple"></div>
  <div class="glow-pink"></div>
  <div class="og-left">
    <div class="og-content">
      <div class="og-lockup">
        <img class="og-logo" src="logo-transparent.png" alt="Noogat">
        <div class="og-copy">
          <div class="og-wordmark">NOOGAT</div>
          <div class="og-tagline">
            Capture notes with Siri.<br>
            <strong>Voice notes that organize themselves.</strong>
          </div>
        </div>
      </div>
      <div class="og-stats">
        <div class="og-stat purple">
          <span class="slabel">Capture time</span>
          <span class="sval">0s</span>
          <span class="sicon">🎙️</span>
        </div>
        <div class="og-stat green">
          <span class="slabel">To start</span>
          <span class="sval">Free</span>
          <span class="sicon">✨</span>
        </div>
        <div class="og-stat pink">
          <span class="slabel">Platform</span>
          <span class="sval">iOS</span>
          <span class="sicon">📱</span>
        </div>
      </div>
    </div>
  </div>
  <div class="og-right">
    <img class="og-phone" src="screenshots/screenshot-01-voice.png" alt="Noogat voice capture screen">
  </div>
  <div class="og-band">
    <span>"Hey Siri, I have a Noogat." — hands-free voice notes, always findable</span>
  </div>
</body>
</html>
```

- [ ] **Step 2: Verify it looks right in browser**

Open in browser: `open /Users/matt/Code/noogat-site/assets/og-image-source.html`

Expected: 1200×630 dark purple canvas with the Noogat logo + wordmark on the left, tilted phone screenshot on the right, gradient band at bottom, three stat tiles.

- [ ] **Step 3: Generate og-image.png via headless Chrome**

```bash
/Applications/Google\ Chrome.app/Contents/MacOS/Google\ Chrome \
  --headless=new \
  --screenshot=/Users/matt/Code/noogat-site/assets/og-image.png \
  --window-size=1200,630 \
  --hide-scrollbars \
  --disable-gpu \
  "file:///Users/matt/Code/noogat-site/assets/og-image-source.html"
```

Expected: `assets/og-image.png` created at approximately 800KB–2MB.

- [ ] **Step 4: Verify dimensions**

```bash
sips -g pixelWidth -g pixelHeight /Users/matt/Code/noogat-site/assets/og-image.png
```

Expected output:
```
pixelWidth: 1200
pixelHeight: 630
```

- [ ] **Step 5: Commit**

```bash
cd /Users/matt/Code/noogat-site
git add assets/og-image-source.html assets/og-image.png
git commit -m "feat: add OG share image (1200×630 dark hero design)"
```

---

### Task 2: Hero — dark background + glow orbs

**Files:**
- Modify: `index.html` (CSS `.hero` block, lines ~116–169)

Replace the light hero background with the dark gradient and add absolutely-positioned radial glow orbs. The hero section needs `position: relative; overflow: hidden` to contain the orbs.

- [ ] **Step 1: Replace hero CSS**

Find and replace the existing `.hero` and `.hero-inner` CSS block (the comment `/* --- Hero --- */` through `.hero-screenshot img { ... }`). Replace with:

```css
/* --- Hero --- */
.hero {
  background: linear-gradient(145deg, #0f0020 0%, #1a0040 45%, #25003a 100%);
  padding: 4rem 0 0;
  position: relative;
  overflow: hidden;
}
.hero-glow {
  position: absolute;
  border-radius: 50%;
  pointer-events: none;
}
.hero-glow--purple {
  top: -120px; right: calc(30% - 60px);
  width: 500px; height: 500px;
  background: radial-gradient(circle, rgba(124,34,217,0.45) 0%, transparent 65%);
}
.hero-glow--pink {
  bottom: 80px; left: -60px;
  width: 340px; height: 340px;
  background: radial-gradient(circle, rgba(201,27,91,0.28) 0%, transparent 65%);
}
.hero-inner {
  display: flex;
  align-items: center;
  gap: 3rem;
  position: relative;
  z-index: 1;
}
.hero-text { flex: 1; min-width: 0; }
.hero-brand {
  display: flex;
  align-items: center;
  gap: 0.75rem;
  margin-bottom: 1.75rem;
}
.hero-brand img {
  width: 56px; height: 56px;
  border-radius: 14px;
  flex-shrink: 0;
}
.hero-wordmark {
  font-size: 2.75rem;
  font-weight: 900;
  letter-spacing: -0.04em;
  line-height: 1;
  background: linear-gradient(135deg, #bf5fff 0%, #ff5c8d 55%, #a3e635 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}
.hero-sub {
  font-size: 1.05rem;
  color: rgba(255,255,255,0.6);
  margin-bottom: 0.6rem;
  line-height: 1.6;
}
.hero-tagline {
  font-size: clamp(1.3rem, 2.5vw, 1.65rem);
  font-weight: 800;
  color: #fff;
  margin: 1.5rem 0 2rem;
  line-height: 1.3;
  letter-spacing: -0.02em;
}
.hero-screenshot {
  flex: 0 0 auto;
  position: relative;
  z-index: 1;
}
.hero-screenshot img {
  border-radius: 2.5rem;
  box-shadow: 0 32px 80px rgba(0,0,0,0.55), 0 0 0 1.5px rgba(255,255,255,0.1);
  max-width: 100%;
  height: auto;
  transform: rotate(2deg);
  display: block;
}
```

- [ ] **Step 2: Add glow divs to hero HTML**

Find the hero section opening tag:
```html
  <section class="hero">
    <div class="container">
```

Replace with:
```html
  <section class="hero">
    <div class="hero-glow hero-glow--purple"></div>
    <div class="hero-glow hero-glow--pink"></div>
    <div class="container">
```

- [ ] **Step 3: Verify in browser**

Open `index.html` in a browser. Expected: deep dark purple hero background with subtle glow orbs, gradient wordmark, white text, phone screenshot with a slight tilt and glow shadow.

- [ ] **Step 4: Commit**

```bash
cd /Users/matt/Code/noogat-site
git add index.html
git commit -m "feat: dark hero background with radial glow orbs"
```

---

### Task 3: Hero — stat tiles + gradient band

**Files:**
- Modify: `index.html`

Add the full-width stat tiles row and gradient Siri band below the hero inner content, still inside the hero section.

- [ ] **Step 1: Add stat tiles + band CSS**

Add after the `.hero-screenshot img` CSS rule:

```css
/* Hero stat tiles */
.hero-stats {
  display: flex;
  gap: 12px;
  padding: 2.5rem 0 0;
  position: relative;
  z-index: 1;
}
.hero-stat {
  flex: 1;
  background: rgba(255,255,255,0.05);
  border: 1px solid rgba(255,255,255,0.12);
  border-radius: 14px;
  padding: 1rem 1.25rem 0.875rem;
  display: flex;
  flex-direction: column;
  min-height: 120px;
}
.hero-stat-label {
  font-size: 0.65rem;
  font-weight: 700;
  letter-spacing: 0.08em;
  text-transform: uppercase;
  color: rgba(255,255,255,0.35);
  line-height: 1;
}
.hero-stat-value {
  font-size: 1.75rem;
  font-weight: 800;
  letter-spacing: -0.02em;
  line-height: 1;
  margin-top: 0.35rem;
}
.hero-stat-icon {
  margin-top: auto;
  padding-top: 0.6rem;
  font-size: 1.75rem;
  line-height: 1;
  opacity: 0.7;
}
.hero-stat--purple .hero-stat-value { color: #bf5fff; }
.hero-stat--green  .hero-stat-value { color: #a3e635; }
.hero-stat--pink   .hero-stat-value { color: #ff5c8d; }

/* Hero gradient band */
.hero-band {
  background: linear-gradient(90deg, var(--brand-purple), var(--brand-pink));
  padding: 0.875rem 0;
  margin-top: 2rem;
  position: relative;
  z-index: 1;
}
.hero-band p {
  text-align: center;
  font-size: 0.95rem;
  font-style: italic;
  font-weight: 500;
  color: rgba(255,255,255,0.92);
  margin: 0;
}
```

- [ ] **Step 2: Add stat tiles + band HTML**

Find this in the hero section:
```html
        </div>
      </div>
    </div>
  </section>

  <!-- HEY SIRI -->
```

Replace with:
```html
        </div>
      </div>
      <div class="hero-stats container">
        <div class="hero-stat hero-stat--purple">
          <span class="hero-stat-label">Capture time</span>
          <span class="hero-stat-value">0s</span>
          <span class="hero-stat-icon">🎙️</span>
        </div>
        <div class="hero-stat hero-stat--green">
          <span class="hero-stat-label">To start</span>
          <span class="hero-stat-value">Free</span>
          <span class="hero-stat-icon">✨</span>
        </div>
        <div class="hero-stat hero-stat--pink">
          <span class="hero-stat-label">Platform</span>
          <span class="hero-stat-value">iOS</span>
          <span class="hero-stat-icon">📱</span>
        </div>
      </div>
      <div class="hero-band">
        <p>"Hey Siri, I have a Noogat." — hands-free voice notes, always findable</p>
      </div>
    </div>
  </section>

  <!-- HEY SIRI -->
```

- [ ] **Step 3: Verify in browser**

Expected: three stat tiles (0s / Free / iOS) with emoji icons below the hero content, then a purple→pink gradient band with the Siri quote.

- [ ] **Step 4: Commit**

```bash
cd /Users/matt/Code/noogat-site
git add index.html
git commit -m "feat: add hero stat tiles and gradient band"
```

---

### Task 4: Hero — mobile responsive

**Files:**
- Modify: `index.html` (the `@media (max-width: 768px)` block)

- [ ] **Step 1: Update responsive CSS for dark hero**

Find the existing `@media (max-width: 768px)` block and replace the hero rules inside it:

```css
@media (max-width: 768px) {
  /* Hero: stack text above screenshot */
  .hero-inner {
    flex-direction: column;
    text-align: center;
  }
  .hero-brand { justify-content: center; }
  .hero-screenshot {
    order: -1;     /* screenshot above text on mobile */
  }
  .hero-screenshot img {
    max-width: 240px;
    transform: rotate(1deg);
  }
  .hero-stats { gap: 8px; }
  .hero-stat { min-height: 100px; padding: 0.875rem 0.875rem 0.75rem; }
  .hero-stat-value { font-size: 1.4rem; }
  .hero-stat-icon { font-size: 1.4rem; }

  /* Hey Siri: stack columns then screenshot */
  .siri-body { flex-direction: column; }
  .siri-columns { grid-template-columns: 1fr; gap: 1.25rem; }
  .siri-screenshot { display: none; }

  /* Features: single column */
  .features-grid { grid-template-columns: 1fr; }

  /* Footer links: wrap naturally */
  .footer-links { flex-direction: column; align-items: center; gap: 0.75rem; }
}
```

- [ ] **Step 2: Test at mobile width**

Open browser, resize to 375px wide (iPhone SE). Expected: screenshot above text, all three stat tiles still visible (may be narrow but readable), gradient band text wraps gracefully.

- [ ] **Step 3: Commit**

```bash
cd /Users/matt/Code/noogat-site
git add index.html
git commit -m "fix: hero mobile layout for dark redesign"
```

---

### Task 5: Scroll animations

**Files:**
- Modify: `index.html`

Add fade-up entrance animations for section content using IntersectionObserver. Respects `prefers-reduced-motion`.

- [ ] **Step 1: Add animation CSS**

Add before the closing `</style>` tag in `<head>`:

```css
/* Scroll animations */
.animate {
  opacity: 0;
  transform: translateY(28px);
  transition: opacity 0.55s ease, transform 0.55s ease;
}
.animate.is-visible {
  opacity: 1;
  transform: none;
}
.animate-delay-1 { transition-delay: 0.1s; }
.animate-delay-2 { transition-delay: 0.2s; }
.animate-delay-3 { transition-delay: 0.3s; }
@media (prefers-reduced-motion: reduce) {
  .animate { opacity: 1; transform: none; transition: none; }
}
```

- [ ] **Step 2: Add animate classes to section elements**

In the HTML, add `class="animate"` (or append it to existing classes) to:

- `.siri-quote` → add `animate` class: `<blockquote class="siri-quote animate">`
- `.siri-columns` → `<div class="siri-columns animate animate-delay-1">`
- `.siri-screenshot` → `<div class="siri-screenshot animate animate-delay-2">`
- `.section-title` (features) → `<h2 class="section-title animate">`
- Each `.feature-card` → add `animate` + stagger: first card `animate animate-delay-1`, second `animate animate-delay-2`, third `animate animate-delay-3`
- `.features-screenshot-wrap` → `<div class="features-screenshot-wrap animate">`
- `.section-title` (FAQ) → `<h2 class="section-title animate">`
- `.faq-list` → `<dl class="faq-list animate animate-delay-1">`

- [ ] **Step 3: Add IntersectionObserver script**

Add before the closing `</body>` tag:

```html
<script>
  (function() {
    var observer = new IntersectionObserver(function(entries) {
      entries.forEach(function(entry) {
        if (entry.isIntersecting) {
          entry.target.classList.add('is-visible');
          observer.unobserve(entry.target);
        }
      });
    }, { threshold: 0.12 });

    document.querySelectorAll('.animate').forEach(function(el) {
      observer.observe(el);
    });
  })();
</script>
```

- [ ] **Step 4: Verify animations**

Open `index.html`, scroll down slowly. Expected: each section's content fades up into view. Feature cards stagger in one after another. Reload and verify hero content is immediately visible (hero elements should NOT have `animate` class — only below-fold sections).

- [ ] **Step 5: Commit**

```bash
cd /Users/matt/Code/noogat-site
git add index.html
git commit -m "feat: add scroll fade-up animations with prefers-reduced-motion support"
```

---

### Task 6: Section polish — visual depth + typography

**Files:**
- Modify: `index.html`

Polish the remaining sections with card depth, hover states, and tighter typography.

- [ ] **Step 1: Feature card hover state + depth**

Find `.feature-card` CSS and replace with:

```css
.feature-card {
  background: var(--surface);
  border: 1px solid var(--border);
  border-radius: 16px;
  padding: 1.75rem;
  text-align: center;
  transition: transform 0.2s ease, box-shadow 0.2s ease;
}
.feature-card:hover {
  transform: translateY(-4px);
  box-shadow: 0 12px 40px rgba(124, 34, 217, 0.15);
}
```

- [ ] **Step 2: Pro section — gradient border card**

Find `.pro-section` CSS and add after it:

```css
.pro-card {
  background: var(--surface);
  border-radius: 20px;
  padding: 2.5rem;
  max-width: 560px;
  position: relative;
}
.pro-card::before {
  content: '';
  position: absolute;
  inset: 0;
  border-radius: 20px;
  padding: 1.5px;
  background: linear-gradient(135deg, var(--brand-purple), var(--brand-pink));
  -webkit-mask: linear-gradient(#fff 0 0) content-box, linear-gradient(#fff 0 0);
  -webkit-mask-composite: xor;
  mask-composite: exclude;
  pointer-events: none;
}
```

Then wrap the Pro section content in HTML:

Find:
```html
      <h2 class="pro-title">Noogat Pro</h2>
      <p class="pro-body">
```

Replace with:
```html
      <div class="pro-card">
      <h2 class="pro-title animate">Noogat Pro</h2>
      <p class="pro-body animate animate-delay-1">
```

And find the closing content of the pro section:
```html
      <!-- Pro features source of truth: claude-inbox/docs/features.json (widgets excluded — not yet released) -->
    </div>
  </section>
```

Replace with:
```html
      <!-- Pro features source of truth: claude-inbox/docs/features.json (widgets excluded — not yet released) -->
      </div>
    </div>
  </section>
```

- [ ] **Step 3: Hey Siri section — glassmorphism copy columns**

Find `.siri-columns p` CSS and replace:

```css
.siri-columns p {
  opacity: 0.9;
  line-height: 1.75;
  margin: 0;
  font-size: 0.975rem;
  background: rgba(255,255,255,0.07);
  border: 1px solid rgba(255,255,255,0.12);
  border-radius: 14px;
  padding: 1.25rem 1.5rem;
  backdrop-filter: blur(4px);
}
```

- [ ] **Step 4: FAQ — tighter question spacing + border treatment**

Find `.faq-list dt` CSS and replace:

```css
.faq-list dt {
  font-size: 1.05rem;
  font-weight: 700;
  color: var(--brand-purple);
  margin-top: 0;
  margin-bottom: 0.4rem;
  padding-top: 1.5rem;
  border-top: 1px solid var(--border);
}
.faq-list dt:first-child {
  padding-top: 0;
  border-top: none;
}
```

- [ ] **Step 5: Verify all sections in browser**

Check: feature cards lift on hover, Pro section has a gradient border, Siri body copy has glass panels, FAQ items have divider lines between them.

- [ ] **Step 6: Commit**

```bash
cd /Users/matt/Code/noogat-site
git add index.html
git commit -m "feat: section polish — card depth, hover states, glassmorphism, Pro gradient border"
```

---

### Task 7: Final review + push

- [ ] **Step 1: Full-page review at desktop (1280px)**

Open `index.html` in browser at full width. Scroll through every section. Check:
- Hero dark bg, glow orbs visible, screenshot tilted, stat tiles and band render
- Siri section glass copy panels readable on purple bg
- Feature cards hover correctly
- Pro card has visible gradient border
- FAQ dividers visible
- Scroll animations fire on each section entry

- [ ] **Step 2: Full-page review at mobile (375px)**

Resize browser to 375px. Check:
- Hero screenshot stacks above text
- Stat tiles still readable (don't overflow)
- Band text doesn't clip
- All sections stack properly

- [ ] **Step 3: Commit and push**

```bash
cd /Users/matt/Code/noogat-site
git add -p   # review any unstaged changes
git push origin main
```

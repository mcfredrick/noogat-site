# Noogat Homepage Redesign Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Replace `noogat-site/index.html` with a rich landing page matching the approved mockup — six full-width sections, brand colors, three App Store screenshots, SEO-complete head, and a static Pro features list.

**Architecture:** Single HTML file linking the existing `_shared.css` for CSS variables and base typography, with a `<style>` block for all layout-specific CSS. No build step, no JS framework, no npm. Each section is a full-width `<section>` element with an inner `.container` div (max-width 1100px) to prevent text from stretching on wide screens.

**Tech Stack:** HTML5, CSS3 (custom properties, flexbox, grid, clamp()), `_shared.css` for tokens

---

## File Map

| Action | File | Purpose |
|---|---|---|
| Copy | `assets/screenshots/screenshot-01-voice.png` | Hero screenshot (voice capture) |
| Copy | `assets/screenshots/screenshot-02-search.png` | Features section screenshot |
| Copy | `assets/screenshots/screenshot-03-home.png` | Hey Siri section screenshot |
| Rewrite | `index.html` | New landing page |

---

## Task 1: Copy Screenshots

**Files:**
- Create: `noogat-site/assets/screenshots/screenshot-01-voice.png`
- Create: `noogat-site/assets/screenshots/screenshot-02-search.png`
- Create: `noogat-site/assets/screenshots/screenshot-03-home.png`

- [ ] **Step 1: Copy and rename screenshots**

```bash
mkdir -p /Users/matt/Code/noogat-site/assets/screenshots
cp "/Users/matt/Code/claude-inbox/scripts/screenshots/en-US/iPhone 17 Pro Max-01_voice.png" \
   /Users/matt/Code/noogat-site/assets/screenshots/screenshot-01-voice.png
cp "/Users/matt/Code/claude-inbox/scripts/screenshots/en-US/iPhone 17 Pro Max-02_search.png" \
   /Users/matt/Code/noogat-site/assets/screenshots/screenshot-02-search.png
cp "/Users/matt/Code/claude-inbox/scripts/screenshots/en-US/iPhone 17 Pro Max-03_home.png" \
   /Users/matt/Code/noogat-site/assets/screenshots/screenshot-03-home.png
```

- [ ] **Step 2: Verify files exist**

```bash
ls -lh /Users/matt/Code/noogat-site/assets/screenshots/
```

Expected: three `.png` files, each 600–900KB.

- [ ] **Step 3: Commit**

```bash
cd /Users/matt/Code/noogat-site
git add assets/screenshots/
git commit -m "feat: add App Store screenshots for landing page"
```

---

## Task 2: HTML Skeleton + Head

**Files:**
- Rewrite: `noogat-site/index.html`

Write the complete `<head>` and empty `<body>` scaffold. All six sections will be added in subsequent tasks.

- [ ] **Step 1: Write the skeleton**

Replace the entire content of `noogat-site/index.html` with:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <link rel="icon" type="image/png" href="/assets/logo-black.png">
  <title>Noogat — The Search Engine for Your Thoughts</title>
  <meta name="description" content="Capture ideas hands-free with Siri, then find them instantly with AI-powered search and auto-tagging. Free for iOS.">
  <link rel="canonical" href="https://noogat.app/">

  <!-- Open Graph -->
  <meta property="og:type" content="website">
  <meta property="og:url" content="https://noogat.app/">
  <meta property="og:title" content="Noogat — The Search Engine for Your Thoughts">
  <meta property="og:description" content="Capture ideas hands-free with Siri, then find them instantly with AI-powered search and auto-tagging. Free for iOS.">
  <meta property="og:image" content="https://noogat.app/assets/screenshots/screenshot-01-voice.png">
  <meta property="og:image:width" content="1320">
  <meta property="og:image:height" content="2868">

  <!-- Twitter Card -->
  <meta name="twitter:card" content="summary_large_image">
  <meta name="twitter:title" content="Noogat — The Search Engine for Your Thoughts">
  <meta name="twitter:description" content="Capture ideas hands-free with Siri, then find them instantly with AI-powered search and auto-tagging. Free for iOS.">
  <meta name="twitter:image" content="https://noogat.app/assets/screenshots/screenshot-01-voice.png">

  <!-- Apple Smart App Banner — shows "Open in App Store" natively in iOS Safari -->
  <meta name="apple-itunes-app" content="app-id=6768415092">

  <!-- Schema.org structured data -->
  <script type="application/ld+json">
  {
    "@context": "https://schema.org",
    "@type": "SoftwareApplication",
    "name": "Noogat",
    "operatingSystem": "iOS",
    "applicationCategory": "ProductivityApplication",
    "offers": {
      "@type": "Offer",
      "price": "0",
      "priceCurrency": "USD"
    },
    "description": "Capture ideas hands-free with Siri, then find them instantly with AI-powered search and auto-tagging.",
    "url": "https://noogat.app"
  }
  </script>

  <link rel="stylesheet" href="_shared.css">
  <style>
    /* Override _shared.css body padding for full-width sections */
    body { padding: 0; }

    .container {
      max-width: 1100px;
      margin: 0 auto;
      padding: 0 1.5rem;
    }

    .btn-cta {
      display: inline-block;
      background: linear-gradient(90deg, #7C22D9, #C91B5B);
      color: #fff;
      text-decoration: none;
      font-weight: 700;
      font-size: 1rem;
      padding: 0.875rem 2rem;
      border-radius: 100px;
      -webkit-text-fill-color: #fff;
      box-shadow: 0 4px 20px rgba(124, 34, 217, 0.35);
      transition: opacity 0.15s;
    }
    .btn-cta:hover { opacity: 0.9; }

    /* Sections added in subsequent tasks */
  </style>

  <!-- Privacy-friendly analytics -->
  <script async src="https://traffic.dayjob.dev/js/pa-rzoUHPXrk_Fzabjb3j1iy.js"></script>
  <script>
    window.plausible=window.plausible||function(){(plausible.q=plausible.q||[]).push(arguments)},plausible.init=plausible.init||function(i){plausible.o=i||{}};
    plausible.init()
  </script>
</head>
<body>
  <!-- sections go here -->
</body>
</html>
```

- [ ] **Step 2: Verify it renders without errors**

Open `noogat-site/index.html` in a browser (empty white page is expected — no sections yet). Check browser console for errors.

- [ ] **Step 3: Commit**

```bash
cd /Users/matt/Code/noogat-site
git add index.html
git commit -m "feat: add SEO-complete head and page skeleton"
```

---

## Task 3: Hero Section

**Files:**
- Modify: `noogat-site/index.html`

- [ ] **Step 1: Add hero HTML inside `<body>`**

Replace `<!-- sections go here -->` with:

```html
  <!-- HERO -->
  <section class="hero">
    <div class="container">
      <div class="hero-inner">
        <div class="hero-text">
          <div class="hero-brand">
            <img src="assets/logo-transparent.png" alt="" width="56" height="56" aria-hidden="true">
            <span class="hero-wordmark">Noogat</span>
          </div>
          <p class="hero-sub">Effortless note-taking to capture your ideas the moment inspiration strikes.</p>
          <p class="hero-sub">AI-powered search to instantly find your ideas again when you need them.</p>
          <p class="hero-tagline">It's like a search engine for your thoughts.</p>
          <a href="https://apps.apple.com/app/noogat/id6768415092" class="btn-cta">
            Download on the App Store
          </a>
        </div>
        <div class="hero-screenshot">
          <img src="assets/screenshots/screenshot-01-voice.png"
               alt="Noogat app showing Siri voice capture in action — the app is listening and saving a new noogat hands-free"
               width="310" height="674" loading="eager">
        </div>
      </div>
    </div>
  </section>

  <!-- remaining sections go here -->
```

- [ ] **Step 2: Add hero CSS inside the `<style>` block, before the closing `</style>` tag**

```css
    /* --- Hero --- */
    .hero {
      background: var(--bg);
      padding: 4rem 0 3rem;
    }
    .hero-inner {
      display: flex;
      align-items: center;
      gap: 3rem;
    }
    .hero-text { flex: 1; min-width: 0; }
    .hero-brand {
      display: flex;
      align-items: center;
      gap: 0.75rem;
      margin-bottom: 1.75rem;
    }
    .hero-brand img {
      width: 56px;
      height: 56px;
      border-radius: 14px;
      flex-shrink: 0;
    }
    .hero-wordmark {
      font-size: 2.75rem;
      font-weight: 900;
      letter-spacing: -0.04em;
      line-height: 1;
      background: linear-gradient(135deg, #7C22D9 0%, #C91B5B 50%, #5B8C00 100%);
      -webkit-background-clip: text;
      -webkit-text-fill-color: transparent;
      background-clip: text;
    }
    .hero-sub {
      font-size: 1.1rem;
      color: var(--text-secondary);
      margin-bottom: 0.6rem;
      line-height: 1.6;
    }
    .hero-tagline {
      font-size: clamp(1.3rem, 2.5vw, 1.65rem);
      font-weight: 800;
      color: var(--brand-purple);
      margin: 1.5rem 0 2rem;
      line-height: 1.3;
      letter-spacing: -0.02em;
    }
    .hero-screenshot { flex: 0 0 auto; }
    .hero-screenshot img {
      border-radius: 2.5rem;
      box-shadow: 0 24px 64px rgba(124, 34, 217, 0.25);
      max-width: 100%;
      height: auto;
    }
```

- [ ] **Step 3: Open in browser and verify**

Check: logo + wordmark visible, two subtitle lines, bold purple tagline, CTA button with gradient, screenshot to the right.

- [ ] **Step 4: Commit**

```bash
cd /Users/matt/Code/noogat-site
git add index.html
git commit -m "feat: add hero section"
```

---

## Task 4: "Hey Siri" Section

**Files:**
- Modify: `noogat-site/index.html`

- [ ] **Step 1: Add HTML — replace `<!-- remaining sections go here -->` with:**

```html
  <!-- HEY SIRI -->
  <section class="siri-section">
    <div class="container">
      <blockquote class="siri-quote">"Hey Siri, I have a Noogat."</blockquote>
      <div class="siri-body">
        <div class="siri-columns">
          <p>You've got a busy brain, and your best ideas always seem to come at the worst times: in the shower, on the road, or in the middle of some other task. Whether you've just come up with the perfect concept for your next big project or you simply need to remember to add "milk" to the grocery list, you need a way to easily capture those thoughts before they escape forever.</p>
          <p>With Noogat for iOS, you can instantly record your notes using Siri voice command. No unlocking your screen, no opening an app, no losing your focus. With semantic search capability and auto-tagging, you can find "that song idea from last Tuesday" three weeks later — without remembering any specific words. No more digging through garbled voice memos or note graveyards.</p>
        </div>
        <div class="siri-screenshot">
          <img src="assets/screenshots/screenshot-03-home.png"
               alt="Noogat home feed showing multiple captured ideas with colorful AI-generated tags"
               width="260" height="564" loading="lazy">
        </div>
      </div>
    </div>
  </section>

  <!-- remaining sections go here -->
```

- [ ] **Step 2: Add CSS inside the `<style>` block:**

```css
    /* --- Hey Siri Section --- */
    .siri-section {
      background: var(--brand-purple);
      color: #fff;
      padding: 5rem 0;
    }
    .siri-quote {
      font-size: clamp(2rem, 4.5vw, 3.25rem);
      font-weight: 900;
      letter-spacing: -0.03em;
      line-height: 1.15;
      margin: 0 0 3rem;
      quotes: none;
    }
    .siri-body {
      display: flex;
      align-items: flex-start;
      gap: 3rem;
    }
    .siri-columns {
      flex: 1;
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 2rem;
    }
    .siri-columns p {
      opacity: 0.9;
      line-height: 1.75;
      margin: 0;
      font-size: 0.975rem;
    }
    .siri-screenshot { flex: 0 0 auto; }
    .siri-screenshot img {
      border-radius: 2rem;
      box-shadow: 0 20px 60px rgba(0, 0, 0, 0.35);
      max-width: 100%;
      height: auto;
    }
```

- [ ] **Step 3: Open in browser and verify**

Check: deep purple background, large quote, two-column body text (left + right), home screenshot visible on the right.

- [ ] **Step 4: Commit**

```bash
cd /Users/matt/Code/noogat-site
git add index.html
git commit -m "feat: add hey siri section"
```

---

## Task 5: Features Section

**Files:**
- Modify: `noogat-site/index.html`

- [ ] **Step 1: Add HTML — replace `<!-- remaining sections go here -->`:**

```html
  <!-- FEATURES -->
  <section class="features-section">
    <div class="container">
      <h2 class="section-title">Features</h2>
      <div class="features-grid">

        <div class="feature-card">
          <div class="feature-icon-wrap" aria-hidden="true">
            <svg width="28" height="28" viewBox="0 0 24 24" fill="currentColor">
              <path d="M12 1a4 4 0 0 0-4 4v7a4 4 0 0 0 8 0V5a4 4 0 0 0-4-4zm0 2a2 2 0 0 1 2 2v7a2 2 0 0 1-4 0V5a2 2 0 0 1 2-2zm-7 9a7 7 0 0 0 6 6.93V21H9v2h6v-2h-2v-2.07A7 7 0 0 0 19 12h-2a5 5 0 0 1-10 0H5z"/>
            </svg>
          </div>
          <h3>Siri-Native Capture</h3>
          <p>Effortlessly record your notes hands-free — no shortcut setup, no app switching, no losing your focus.</p>
        </div>

        <div class="feature-card">
          <div class="feature-icon-wrap" aria-hidden="true">
            <svg width="28" height="28" viewBox="0 0 24 24" fill="currentColor">
              <path d="M21.41 11.58l-9-9A2 2 0 0 0 11 2H4a2 2 0 0 0-2 2v7a2 2 0 0 0 .59 1.42l9 9A2 2 0 0 0 13 22a2 2 0 0 0 1.41-.59l7-7A2 2 0 0 0 22 13a2 2 0 0 0-.59-1.42zM13 20l-9-9V4h7l9 9-7 7zM6.5 7a1.5 1.5 0 1 1 0-3 1.5 1.5 0 0 1 0 3z"/>
            </svg>
          </div>
          <h3>AI Auto-Tagging</h3>
          <p>Every idea is automatically tagged and categorized for easy access.</p>
        </div>

        <div class="feature-card">
          <div class="feature-icon-wrap" aria-hidden="true">
            <svg width="28" height="28" viewBox="0 0 24 24" fill="currentColor">
              <path d="M15.5 14h-.79l-.28-.27A6.47 6.47 0 0 0 16 9.5 6.5 6.5 0 1 0 9.5 16c1.61 0 3.09-.59 4.23-1.57l.27.28v.79l5 4.99L20.49 19l-4.99-5zm-6 0C7.01 14 5 11.99 5 9.5S7.01 5 9.5 5 14 7.01 14 9.5 11.99 14 9.5 14z"/>
            </svg>
          </div>
          <h3>Full-Text Search</h3>
          <p>Search across all your ideas instantly, including by tag or semantically.</p>
        </div>

      </div>

      <div class="features-screenshot-wrap">
        <img src="assets/screenshots/screenshot-02-search.png"
             alt="Noogat semantic search results showing related ideas grouped by tag — 'A search engine for your brain'"
             width="310" height="674" loading="lazy">
      </div>
    </div>
  </section>

  <!-- remaining sections go here -->
```

- [ ] **Step 2: Add CSS inside the `<style>` block:**

```css
    /* --- Features Section --- */
    .features-section {
      background: var(--surface-secondary);
      padding: 5rem 0;
    }
    .section-title {
      font-size: clamp(1.75rem, 3vw, 2.5rem);
      font-weight: 900;
      letter-spacing: -0.03em;
      color: var(--text);
      margin: 0 0 2.5rem;
    }
    .features-grid {
      display: grid;
      grid-template-columns: repeat(3, 1fr);
      gap: 1.5rem;
      margin-bottom: 3rem;
    }
    .feature-card {
      background: var(--surface);
      border: 1px solid var(--border);
      border-radius: 16px;
      padding: 1.75rem;
      text-align: center;
    }
    .feature-icon-wrap {
      width: 64px;
      height: 64px;
      background: #fff;
      border-radius: 50%;
      display: flex;
      align-items: center;
      justify-content: center;
      margin: 0 auto 1rem;
      color: var(--brand-purple);
      box-shadow: 0 2px 12px rgba(124, 34, 217, 0.15);
    }
    .feature-card h3 {
      font-size: 0.8rem;
      font-weight: 800;
      text-transform: uppercase;
      letter-spacing: 0.08em;
      color: var(--brand-purple);
      margin-bottom: 0.6rem;
    }
    .feature-card p {
      font-size: 0.9rem;
      color: var(--text-secondary);
      line-height: 1.6;
      margin: 0;
    }
    .features-screenshot-wrap {
      text-align: center;
      margin-top: 1rem;
    }
    .features-screenshot-wrap img {
      border-radius: 2rem;
      box-shadow: 0 20px 60px rgba(124, 34, 217, 0.18);
      max-width: 100%;
      height: auto;
    }
```

- [ ] **Step 3: Open in browser and verify**

Check: lavender background, "Features" heading, three equal cards with icon circles, feature labels in uppercase purple, search screenshot centered below.

- [ ] **Step 4: Commit**

```bash
cd /Users/matt/Code/noogat-site
git add index.html
git commit -m "feat: add features section"
```

---

## Task 6: Noogat Pro Section

**Files:**
- Modify: `noogat-site/index.html`

- [ ] **Step 1: Add HTML — replace `<!-- remaining sections go here -->`:**

```html
  <!-- NOOGAT PRO -->
  <section class="pro-section">
    <div class="container">
      <h2 class="pro-title">Noogat Pro</h2>
      <p class="pro-body">
        The basic level of Noogat is completely free to use. Upgrade to the <strong>Pro tier</strong> for
        <strong>$4.99/month</strong> or <strong>$49.99/year</strong> to get advanced features:
      </p>
      <ul class="pro-features">
        <li><span class="pro-emoji">✨</span> Semantic search</li>
        <li><span class="pro-emoji">📦</span> Bulk export noogats</li>
        <li><span class="pro-emoji">🔗</span> Related noogats</li>
      </ul>
      <!-- Pro features source of truth: claude-inbox/docs/features.json (widgets excluded — not yet released) -->
    </div>
  </section>

  <!-- remaining sections go here -->
```

- [ ] **Step 2: Add CSS inside the `<style>` block:**

```css
    /* --- Pro Section --- */
    .pro-section {
      background: var(--surface);
      padding: 5rem 0;
    }
    .pro-title {
      font-size: clamp(1.75rem, 3vw, 2.5rem);
      font-weight: 900;
      letter-spacing: -0.03em;
      color: var(--text);
      margin: 0 0 1rem;
    }
    .pro-body {
      font-size: 1.05rem;
      max-width: 620px;
      margin-bottom: 1.5rem;
      line-height: 1.7;
    }
    .pro-features {
      list-style: none;
      padding: 0;
      margin-bottom: 2rem;
    }
    .pro-features li {
      font-size: 1.05rem;
      font-weight: 600;
      padding: 0.5rem 0;
      border-bottom: 1px solid var(--border);
      display: flex;
      align-items: center;
      gap: 0.75rem;
      max-width: 400px;
    }
    .pro-features li:last-child { border-bottom: none; }
    .pro-emoji { font-size: 1.25rem; }
```

- [ ] **Step 3: Open in browser and verify**

Check: white background, "Noogat Pro" heading, pricing copy with bolded amounts, three Pro features in a list.

- [ ] **Step 4: Commit**

```bash
cd /Users/matt/Code/noogat-site
git add index.html
git commit -m "feat: add noogat pro section"
```

---

## Task 7: FAQ + Footer

**Files:**
- Modify: `noogat-site/index.html`

- [ ] **Step 1: Add HTML — replace `<!-- remaining sections go here -->`:**

```html
  <!-- FAQ -->
  <section class="faq-section">
    <div class="container">
      <h2 class="section-title">FAQ</h2>
      <dl class="faq-list">

        <dt>What is Noogat?</dt>
        <dd>Noogat is an app for iOS devices that allows you to use Apple's Siri voice command to effortlessly capture your notes. You can also type your thoughts directly in the app. Noogat uses AI auto-tagging and semantic search to allow you to find those ideas later so they don't get lost. The tags are color-coded for easy scanning and connecting related thoughts. You are also able to create your own tags so you can make sure your notes make sense for <em>you</em>.</dd>

        <dt>Where can I get Noogat?</dt>
        <dd>Noogat is available for iPhone and iPad on the <a href="https://apps.apple.com/app/noogat/id6768415092">Apple App Store</a>. Noogat is not yet available for Android devices.</dd>

        <dt>Is Noogat free?</dt>
        <dd>Yes! The basic tier of Noogat is completely free to use. If you are looking for more features, you can upgrade to the Pro tier for $4.99/month or $49.99/year.</dd>

        <dt>Are you going to sell my Noogats?</dt>
        <dd>Absolutely not. We will never sell your data to advertisers, nor will we ever push ads on our platform. See our <a href="privacy/">Privacy Policy</a> for full details.</dd>

      </dl>
    </div>
  </section>

  <!-- FOOTER -->
  <footer class="site-footer">
    <div class="container">
      <nav class="footer-links" aria-label="Footer">
        <a href="privacy/">Privacy Policy</a>
        <a href="terms/">Terms of Service</a>
        <a href="mailto:support@dayjoy.dev">Contact</a>
      </nav>
      <p class="footer-copy">&copy; 2026 Noogat</p>
    </div>
  </footer>
```

- [ ] **Step 2: Add CSS inside the `<style>` block:**

```css
    /* --- FAQ Section --- */
    .faq-section {
      background: var(--surface);
      padding: 5rem 0;
      border-top: 1px solid var(--border);
    }
    .faq-list {
      max-width: 720px;
    }
    .faq-list dt {
      font-size: 1.05rem;
      font-weight: 700;
      color: var(--brand-purple);
      margin-top: 1.75rem;
      margin-bottom: 0.4rem;
    }
    .faq-list dt:first-child { margin-top: 0; }
    .faq-list dd {
      margin: 0;
      color: var(--text);
      line-height: 1.75;
      font-size: 0.975rem;
    }
    .faq-list dd a { color: var(--brand-purple); }

    /* --- Footer --- */
    .site-footer {
      background: var(--surface-secondary);
      padding: 2.5rem 0;
      border-top: 1px solid var(--border);
    }
    .footer-links {
      display: flex;
      gap: 1.5rem;
      justify-content: center;
      flex-wrap: wrap;
      margin-bottom: 0.75rem;
    }
    .footer-links a {
      color: var(--text-secondary);
      text-decoration: none;
      font-size: 0.875rem;
    }
    .footer-links a:hover { color: var(--brand-purple); }
    .footer-copy {
      text-align: center;
      font-size: 0.8rem;
      color: var(--text-secondary);
      margin: 0;
    }
```

- [ ] **Step 3: Open in browser and verify**

Check: FAQ questions in brand purple, four Q&A pairs, footer with three links + copyright, no raw "Click here" text.

- [ ] **Step 4: Commit**

```bash
cd /Users/matt/Code/noogat-site
git add index.html
git commit -m "feat: add faq and footer"
```

---

## Task 8: Mobile Responsive CSS

**Files:**
- Modify: `noogat-site/index.html`

- [ ] **Step 1: Add responsive breakpoints inside the `<style>` block, at the very end:**

```css
    /* --- Responsive --- */
    @media (max-width: 768px) {
      /* Hero: stack text above screenshot */
      .hero-inner {
        flex-direction: column;
        text-align: center;
      }
      .hero-brand { justify-content: center; }
      .hero-screenshot img { max-width: 280px; }

      /* Hey Siri: stack columns then screenshot */
      .siri-body { flex-direction: column; }
      .siri-columns { grid-template-columns: 1fr; gap: 1.25rem; }
      .siri-screenshot { display: none; } /* screenshot already shown in hero */

      /* Features: single column */
      .features-grid { grid-template-columns: 1fr; }

      /* Footer links: wrap naturally */
      .footer-links { flex-direction: column; align-items: center; gap: 0.75rem; }
    }
```

- [ ] **Step 2: Verify mobile layout**

In browser DevTools, toggle responsive mode at 390px width (iPhone 14/15/16 viewport). Check:
- Hero text stacks above screenshot
- Hey Siri section reads as single column
- Features cards stack vertically
- Footer links stack vertically

- [ ] **Step 3: Commit**

```bash
cd /Users/matt/Code/noogat-site
git add index.html
git commit -m "feat: add mobile responsive breakpoints"
```

---

## Task 9: Serve Locally

- [ ] **Step 1: Start a local HTTP server from the noogat-site directory**

```bash
cd /Users/matt/Code/noogat-site && python3 -m http.server 8080
```

- [ ] **Step 2: Open in browser**

Navigate to: `http://localhost:8080`

Verify each section top to bottom:
- [ ] Hero: wordmark gradient, two subtitles, bold tagline, purple CTA button, voice screenshot
- [ ] Hey Siri: deep purple bg, large quote, two columns of body copy, home screenshot
- [ ] Features: lavender bg, three cards with icon circles, search screenshot below
- [ ] Noogat Pro: white bg, $4.99/month pricing, three-item Pro feature list
- [ ] FAQ: four Q&As, questions in purple, "Apple App Store" capitalized, privacy link goes to `/privacy/`
- [ ] Footer: three links + copyright

- [ ] **Step 3: Check browser console**

No 404 errors for images or CSS. No JS errors.

---

## Task 10: robots.txt — Allow All Crawlers Including AI Bots

**Files:**
- Create: `noogat-site/robots.txt`

No `robots.txt` currently exists. Add one that explicitly permits all crawlers, including AI search bots (GPTBot, PerplexityBot, ClaudeBot, Googlebot). Explicit permission future-proofs against any default behavior changes.

- [ ] **Step 1: Create `noogat-site/robots.txt`**

```
User-agent: *
Allow: /

# AI search crawlers — explicitly permitted for generative search indexing
User-agent: GPTBot
Allow: /

User-agent: PerplexityBot
Allow: /

User-agent: ClaudeBot
Allow: /

User-agent: GoogleOther
Allow: /

Sitemap: https://noogat.app/sitemap.xml
```

- [ ] **Step 2: Commit**

```bash
cd /Users/matt/Code/noogat-site
git add robots.txt
git commit -m "feat: add robots.txt permitting all crawlers including AI bots"
```

---

## Task 11: FAQPage Schema — Feed AI Overviews and Perplexity

**Files:**
- Modify: `noogat-site/index.html`

Add a second `<script type="application/ld+json">` block to `<head>` with `FAQPage` schema. This is how Google AI Overviews, Perplexity, and other generative engines confidently extract and surface the Q&A pairs from our FAQ section as authoritative answers.

- [ ] **Step 1: Add FAQPage JSON-LD block in `<head>`, immediately after the existing `SoftwareApplication` script block**

```html
  <script type="application/ld+json">
  {
    "@context": "https://schema.org",
    "@type": "FAQPage",
    "mainEntity": [
      {
        "@type": "Question",
        "name": "What is Noogat?",
        "acceptedAnswer": {
          "@type": "Answer",
          "text": "Noogat is an app for iOS devices that allows you to use Apple's Siri voice command to effortlessly capture your notes. You can also type your thoughts directly in the app. Noogat uses AI auto-tagging and semantic search to allow you to find those ideas later so they don't get lost. The tags are color-coded for easy scanning and connecting related thoughts. You are also able to create your own tags so you can make sure your notes make sense for you."
        }
      },
      {
        "@type": "Question",
        "name": "Where can I get Noogat?",
        "acceptedAnswer": {
          "@type": "Answer",
          "text": "Noogat is available for iPhone and iPad on the Apple App Store. Noogat is not yet available for Android devices."
        }
      },
      {
        "@type": "Question",
        "name": "Is Noogat free?",
        "acceptedAnswer": {
          "@type": "Answer",
          "text": "Yes. The basic tier of Noogat is completely free to use. You can upgrade to the Pro tier for $4.99/month or $49.99/year for advanced features including semantic search, bulk export, and related noogats."
        }
      },
      {
        "@type": "Question",
        "name": "Does Noogat sell user data?",
        "acceptedAnswer": {
          "@type": "Answer",
          "text": "No. Noogat will never sell user data to advertisers and does not serve ads."
        }
      }
    ]
  }
  </script>
```

- [ ] **Step 2: Verify JSON is valid**

Paste the JSON-LD block into https://validator.schema.org/ (or use the browser console: copy the JSON content and run `JSON.parse(...)` — should return an object with no errors).

- [ ] **Step 3: Commit**

```bash
cd /Users/matt/Code/noogat-site
git add index.html
git commit -m "feat: add FAQPage schema for generative search"
```

---

## Task 12: llms.txt — Positioning Document for LLM Crawlers

**Files:**
- Create: `noogat-site/llms.txt`

`llms.txt` is an emerging standard (llmstxt.org) that gives LLM-powered search engines a structured plain-text summary of a site — what it is, who it's for, and why it exists. Unlike standard SEO meta tags, this file is written *for AI systems* and can include positioning context and competitive framing that helps generative engines route relevant queries to Noogat.

- [ ] **Step 1: Create `noogat-site/llms.txt`**

```
# Noogat

> Noogat is a voice-first idea capture app for iPhone and iPad. Say "Hey Siri, I have a Noogat" and your thought is saved instantly — no unlocking your screen, no opening an app, no losing your focus. AI auto-tagging and semantic search mean you can find any idea later without remembering the exact words.

## Who Noogat is for

Noogat is for people whose best ideas arrive at inconvenient moments — in the shower, on the road, mid-conversation, or in the middle of another task. It is designed for people who want to capture ideas effortlessly but do not want to invent or maintain an organizational system. Unlike note-taking apps that require you to decide on folders, notebooks, tags, or hierarchies before you can start, Noogat handles all organization automatically. You capture; the AI categorizes.

Noogat is the right choice when:
- You lose ideas because reaching for your phone breaks your flow
- You have tried other note apps but abandoned them because maintaining the system felt like work
- You want to find an idea you captured weeks ago without remembering any specific words
- You want something that stays out of the way until you need it

## What makes Noogat different

- **Zero-friction capture:** Siri AppIntents integration means capturing a thought requires only your voice — no app to open, no shortcut to configure
- **No organizational overhead:** AI auto-tagging categorizes every idea automatically; you never need to decide where something goes
- **Meaning-based retrieval:** Semantic search finds ideas by concept, not just keyword — "that thing I was thinking about on the drive home" will surface the right note
- **Designed for the capture moment, not the review session:** Noogat optimizes for the 3 seconds it takes to have and save an idea, not for long reading sessions

## Pricing

- Free tier: unlimited captures, AI auto-tagging, keyword search, tag filtering, idea editing, sharing
- Pro tier: $4.99/month or $49.99/year — adds semantic search, bulk export, and related noogats
- 14-day free trial for Pro

## Platform

iOS and iPadOS only. Requires iOS 17 or later. Available on the Apple App Store.

## Key pages

- Homepage: https://noogat.app/
- Privacy Policy: https://noogat.app/privacy/
- Terms of Service: https://noogat.app/terms/
- App Store listing: https://apps.apple.com/app/noogat/id6768415092
```

- [ ] **Step 2: Commit**

```bash
cd /Users/matt/Code/noogat-site
git add llms.txt
git commit -m "feat: add llms.txt for generative search positioning"
```

---

## Updated Task 9: Serve Locally

- [ ] **Step 1: Start a local HTTP server from the noogat-site directory**

```bash
cd /Users/matt/Code/noogat-site && python3 -m http.server 8080
```

- [ ] **Step 2: Open in browser**

Navigate to: `http://localhost:8080`

Verify each section top to bottom:
- [ ] Hero: wordmark gradient, two subtitles, bold tagline, purple CTA button, voice screenshot
- [ ] Hey Siri: deep purple bg, large quote, two columns of body copy, home screenshot
- [ ] Features: lavender bg, three cards with icon circles, search screenshot below
- [ ] Noogat Pro: white bg, $4.99/month pricing, three-item Pro feature list
- [ ] FAQ: four Q&As, questions in purple, "Apple App Store" capitalized, privacy link goes to `/privacy/`
- [ ] Footer: three links + copyright

- [ ] **Step 3: Verify supporting files**

```bash
curl -s http://localhost:8080/robots.txt | head -5
curl -s http://localhost:8080/llms.txt | head -5
```

Expected: first lines of each file, no 404.

- [ ] **Step 4: Check browser console**

No 404 errors for images or CSS. No JS errors.

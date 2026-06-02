# Noogat Homepage Redesign — Design Spec

**Date:** 2026-06-01  
**Branch:** `feat/homepage-redesign` (noogat-site repo)  
**Replaces:** `index.html`

---

## Overview

Replace the current minimal `index.html` with a richer landing page that follows the Canva mockup layout and copy, uses exact Noogat brand colors, incorporates three App Store screenshots, and follows current SEO best practices. `landing-page.html` is left untouched.

---

## Architecture

- **Target file:** `noogat-site/index.html` — full rewrite
- **New assets:** Copy three screenshots from `claude-inbox/scripts/screenshots/en-US/` into `noogat-site/assets/screenshots/`, renaming to remove spaces:
  - `iPhone 17 Pro Max-01_voice.png` → `screenshot-01-voice.png`
  - `iPhone 17 Pro Max-02_search.png` → `screenshot-02-search.png`
  - `iPhone 17 Pro Max-03_home.png` → `screenshot-03-home.png`
- **Features list:** Static HTML listing the three currently-shipped Pro features. Not wired to `features.json` yet — the GHA automation (triggered on `build/*` release tags) is a separate follow-up project.
- **No build step** — pure HTML/CSS, no JS framework, no npm.

---

## Color Tokens

All colors come from `DESIGN_SYSTEM.md` / `_shared.css`. Do not use raw hex values outside of CSS custom property definitions.

```css
:root {
  --brand-purple:       #7C22D9;
  --brand-purple-light: #BF5FFF;
  --brand-green:        #5B8C00;
  --brand-green-light:  #A3E635;
  --brand-pink:         #C91B5B;
  --brand-pink-light:   #FF5C8D;
  --bg-primary:         #F8F5FF;
  --surface:            #FFFFFF;
  --surface-secondary:  #F0EBF8;
  --border:             #E5D9F7;
  --gradient-hero:      linear-gradient(135deg, #7C22D9 0%, #C91B5B 50%, #5B8C00 100%);
  --gradient-cta:       linear-gradient(90deg, #7C22D9, #C91B5B);
}
```

---

## Typography

System font stack (`-apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif`) — no Google Fonts dependency, no render-blocking requests.

---

## Page Sections

### 1. Hero

**Background:** `--bg-primary` (`#F8F5FF`)  
**Layout:** Two-column on desktop (text left, screenshot right); stacked on mobile (text above, screenshot below)

Content:
- **Wordmark:** "NOOGAT" in large display text with `--gradient-hero` applied as a text gradient
- **Subtitle line 1:** "Effortless note-taking to capture your ideas the moment inspiration strikes."
- **Subtitle line 2:** "AI-powered search to instantly find your ideas again when you need them."
- **Tagline:** "It's like a search engine for your thoughts." (bold, larger)
- **CTA button:** "Download on the App Store" — `--gradient-cta` background, white text, App Store icon, links to App Store listing
- **Screenshot:** `01_voice.png` (iPhone 17 Pro Max voice capture screen)

---

### 2. "Hey Siri" Section

**Background:** `--brand-purple` (`#7C22D9`), white text  
**Layout:** Large quote above; two-column text + screenshot below

Content:
- **Headline:** `"Hey Siri, I have a Noogat."` (large display quote)
- **Left column body copy:**
  > You've got a busy brain, and your best ideas always seem to come at the worst times: in the shower, on the road, or in the middle of some other task. Whether you've just come up with the perfect concept for your next big project or you simply need to remember to add "milk" to the grocery list, you need a way to easily capture those thoughts before they escape forever.
- **Right column body copy:**
  > With Noogat for iOS, you can instantly record your notes using Siri voice command. No unlocking your screen, no opening an app, no losing your focus. With semantic search capability and auto-tagging, you can find "that song idea from last Tuesday" three weeks later — without remembering any specific words. No more digging through garbled voice memos or note graveyards.
- **Screenshot:** `03_home.png` (home feed showing tagged noogats) — placed alongside or below the two-column copy

---

### 3. Features Section

**Background:** `--surface-secondary` (`#F0EBF8`)  
**Layout:** "Features" heading above three equal-width cards in a row (stacked on mobile)

Cards:

| Icon | Label | Body |
|---|---|---|
| Microphone (⚪ circle) | **SIRI-NATIVE CAPTURE** | Effortlessly record your notes hands-free — no shortcut setup, no app switching, no losing your focus. |
| Tag (⚪ circle) | **AI AUTO-TAGGING** | Every idea is automatically tagged and categorized for easy access. |
| Magnifier (⚪ circle) | **FULL-TEXT SEARCH** | Search across all your ideas instantly, including by tag or semantically. |

- Icon circles: white background, `--brand-purple` icon color
- Card labels: uppercase, `--brand-purple`, bold
- Screenshot: `02_search.png` placed below the cards (full-width or centered), showing semantic search in action

---

### 4. Noogat Pro Section

**Background:** `--surface` (`#FFFFFF`)  
**Layout:** Heading + prose + feature list

Content:
- **Heading:** "Noogat Pro"
- **Body:**
  > The basic level of Noogat is completely free to use. Upgrade to the Pro tier for **$4.99/month** or **$49.99/year** to get advanced features:
- **Pro features list** (static, shipped features only — widgets excluded):
  - ✨ Semantic search
  - 📦 Bulk export noogats
  - 🔗 Related noogats
- Note: This list is manually maintained until the GHA automation follow-up project is complete. When features ship, update this list and add an entry to `SHIPPED_FEATURES.md`.

---

### 5. FAQ Section

**Background:** `--surface` (`#FFFFFF`)  
**Layout:** "FAQ" heading + Q&A list

Questions use `--brand-purple` color. Answers use default body text.

| Question | Answer |
|---|---|
| What is Noogat? | Noogat is an app for iOS devices that allows you to use Apple's Siri voice command to effortlessly capture your notes. You can also type your thoughts directly in the app. Noogat uses AI auto-tagging and semantic search to allow you to find those ideas later so they don't get lost. The tags are color-coded for easy scanning and connecting related thoughts. You are also able to create your own tags so you can make sure your notes make sense for *you*. |
| Where can I get Noogat? | Noogat is available for iPhone and iPad on the **Apple App Store**. Noogat is not yet available for Android devices. |
| Is Noogat free? | Yes! The basic tier of Noogat is completely free to use. If you are looking for more features, you can upgrade to the Pro tier for $4.99/month or $49.99/year. |
| Are you going to sell my Noogats? | Absolutely not. We will never sell your data to advertisers, nor will we ever push ads on our platform. See our [Privacy Policy](/privacy/) for full details. |

Copy corrections applied vs. mockup:
- "Apple app store" → "Apple App Store"
- "$5/month" → "$4.99/month" (both in Pro section and FAQ)
- "advanced features :" → "advanced features:" (space before colon removed)
- Stray "I" at end of first pricing sentence removed
- "Click here for a full overview of our privacy policy" → "See our [Privacy Policy](/privacy/) for full details."

---

### 6. Footer

**Background:** `--surface-secondary` or dark (`--bg-primary` dark variant optional)  
**Layout:** Centered links + copyright

Links:
- [Privacy Policy](/privacy/)
- [Terms of Service](/terms/)
- Contact (mailto link)

---

## SEO

### `<head>` requirements

```html
<title>Noogat — The Search Engine for Your Thoughts</title>
<meta name="description" content="Capture ideas hands-free with Siri, then find them instantly with AI-powered search and auto-tagging. Free for iOS.">
<link rel="canonical" href="https://noogat.app/">

<!-- Open Graph -->
<meta property="og:type" content="website">
<meta property="og:url" content="https://noogat.app/">
<meta property="og:title" content="Noogat — The Search Engine for Your Thoughts">
<meta property="og:description" content="Capture ideas hands-free with Siri, then find them instantly with AI-powered search and auto-tagging. Free for iOS.">
<meta property="og:image" content="https://noogat.app/assets/screenshots/screenshot-01-voice.png">

<!-- Twitter Card -->
<meta name="twitter:card" content="summary_large_image">
<meta name="twitter:title" content="Noogat — The Search Engine for Your Thoughts">
<meta name="twitter:description" content="Capture ideas hands-free with Siri, then find them instantly with AI-powered search and auto-tagging. Free for iOS.">
<meta name="twitter:image" content="https://noogat.app/assets/screenshots/screenshot-01-voice.png">

<!-- Apple Smart App Banner -->
<meta name="apple-itunes-app" content="app-id=6768415092">
```

### Structured data (JSON-LD)

```json
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
```

### Image requirements

- All `<img>` tags must have descriptive `alt` text
- Explicit `width` and `height` attributes on all images (prevents layout shift)
- `loading="lazy"` on all below-fold images (sections 2–6)
- `loading="eager"` on the hero screenshot (above the fold)

---

## What Is Out of Scope

- `landing-page.html` — untouched
- `features.json` → noogat-site automation (GHA follow-up project)
- Dark mode for the website (the site is light-mode only for now)
- Any pages other than `index.html`

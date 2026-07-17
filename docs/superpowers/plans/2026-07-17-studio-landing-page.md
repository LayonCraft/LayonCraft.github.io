# LayonCraft Studio Landing Page Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Replace the placeholder `index.html` with a static, no-build-tool landing page for LayonCraft that introduces the studio and showcases its first title, Slide Block.

**Architecture:** Single static page (`index.html` + `style.css` + `script.js`), no framework, no build step, served directly by GitHub Pages from the repo root.

**Tech Stack:** Plain HTML5, CSS3 (custom properties), vanilla JS (`IntersectionObserver`), Google Fonts (Space Grotesk) via CDN link.

## Global Constraints

- English-only copy.
- No build tooling of any kind — files are served as-is by GitHub Pages.
- Store link and social links are placeholders (`href="#"`), each marked with an HTML comment noting it needs to be filled in later.
- Portfolio card markup must be structured so a second card can be added later by duplicating one `.card` block.
- Page must be fully functional (content visible, no broken layout) with JavaScript disabled.
- Color system: `--bg:#0F0F14`, `--bg-card:#1A1A22`, `--primary:#FF6B35`, `--accent:#FF3D8A`, `--text:#F5F5F5`, `--text-muted:#A0A0AA`.
- Headline font: Space Grotesk (Google Fonts) with `system-ui, sans-serif` fallback. Body font: system font stack.
- Since this is a static content page with no test framework, "test" steps below mean **opening `index.html` in a browser and visually verifying** specific, listed criteria — not automated tests.

---

### Task 1: Base scaffolding — file structure, design tokens, HTML skeleton

**Files:**
- Create: `style.css`
- Create: `script.js` (empty stub for now)
- Modify: `index.html` (full replacement)

**Interfaces:**
- Produces: CSS custom properties `--bg`, `--bg-card`, `--primary`, `--accent`, `--text`, `--text-muted`, `--font-heading`, `--font-body` on `:root`, available to all later tasks.
- Produces: HTML skeleton with `<header class="hero">`, `<main>` containing `<section class="portfolio">`, and `<footer class="site-footer">` — later tasks fill these in.
- Produces: `<html>` gets a `js` class added by an inline script the moment JS runs, so CSS can distinguish JS-enabled vs no-JS state (used by Task 6).

- [ ] **Step 1: Write `style.css` with reset and design tokens**

```css
/* style.css */
:root {
  --bg: #0F0F14;
  --bg-card: #1A1A22;
  --primary: #FF6B35;
  --accent: #FF3D8A;
  --text: #F5F5F5;
  --text-muted: #A0A0AA;
  --font-heading: 'Space Grotesk', system-ui, sans-serif;
  --font-body: system-ui, -apple-system, 'Segoe UI', sans-serif;
}

* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

html, body {
  height: 100%;
}

body {
  background: var(--bg);
  color: var(--text);
  font-family: var(--font-body);
  line-height: 1.5;
}

img {
  max-width: 100%;
  display: block;
}

a {
  color: inherit;
}
```

- [ ] **Step 2: Write `index.html` skeleton**

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>LayonCraft — Indie Game Studio</title>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Space+Grotesk:wght@500;700&display=swap" rel="stylesheet">
  <link rel="stylesheet" href="style.css">
  <script>document.documentElement.classList.add('js');</script>
</head>
<body>
  <header class="hero">
    <!-- Task 2 fills this in -->
  </header>

  <main>
    <section class="portfolio">
      <!-- Task 3 fills this in -->
    </section>
  </main>

  <footer class="site-footer">
    <!-- Task 4 fills this in -->
  </footer>

  <script src="script.js"></script>
</body>
</html>
```

- [ ] **Step 3: Create empty `script.js` stub**

```js
// script.js
```

- [ ] **Step 4: Verify in browser**

Open `index.html` directly in a browser (double-click or drag into a browser window).

Expected:
- Page background is dark charcoal (near-black), not white.
- No console errors (open DevTools console, confirm empty).
- View page source shows `<html class="js">` (confirms the inline script ran).

- [ ] **Step 5: Commit**

```bash
git add index.html style.css script.js
git commit -m "Scaffold static page structure and design tokens"
```

---

### Task 2: Hero section

**Files:**
- Modify: `index.html` (fill in `<header class="hero">`)
- Modify: `style.css` (append hero styles)

**Interfaces:**
- Consumes: `--bg`, `--primary`, `--accent`, `--text`, `--font-heading` from Task 1.
- Produces: `.hero`, `.hero__blob`, `.hero__wordmark`, `.hero__tagline` classes — no later task depends on these directly, but Task 5 (responsive) adjusts `.hero` sizing.

- [ ] **Step 1: Fill in hero markup in `index.html`**

Replace the `<header class="hero">` block with:

```html
  <header class="hero">
    <div class="hero__blob" aria-hidden="true"></div>
    <h1 class="hero__wordmark">LAYONCRAFT</h1>
    <p class="hero__tagline">Crafting playful puzzle experiences.</p>
  </header>
```

- [ ] **Step 2: Add hero styles to `style.css`**

```css
/* Hero */
.hero {
  position: relative;
  overflow: hidden;
  min-height: 60vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  text-align: center;
  padding: 4rem 1.5rem;
}

.hero__blob {
  position: absolute;
  top: 50%;
  left: 50%;
  width: 60rem;
  height: 60rem;
  transform: translate(-50%, -50%);
  background: radial-gradient(circle, var(--primary) 0%, var(--accent) 45%, transparent 70%);
  opacity: 0.25;
  filter: blur(60px);
  z-index: 0;
}

.hero__wordmark {
  position: relative;
  z-index: 1;
  font-family: var(--font-heading);
  font-weight: 700;
  font-size: clamp(2.5rem, 8vw, 5rem);
  letter-spacing: 0.05em;
}

.hero__tagline {
  position: relative;
  z-index: 1;
  margin-top: 1rem;
  font-size: clamp(1rem, 2vw, 1.25rem);
  color: var(--text-muted);
}
```

- [ ] **Step 3: Verify in browser**

Reload `index.html`.

Expected:
- "LAYONCRAFT" appears large, bold, centered.
- Tagline "Crafting playful puzzle experiences." appears below it in muted gray.
- A soft blurred orange-to-pink glow is visible behind the text, centered.
- No horizontal scrollbar appears.

- [ ] **Step 4: Commit**

```bash
git add index.html style.css
git commit -m "Add hero section with wordmark, tagline, and gradient blob"
```

---

### Task 3: Portfolio card section

**Files:**
- Modify: `index.html` (fill in `<section class="portfolio">`)
- Modify: `style.css` (append portfolio/card styles)

**Interfaces:**
- Consumes: `--bg-card`, `--primary`, `--accent`, `--text`, `--text-muted`, `--font-heading` from Task 1.
- Produces: `.portfolio`, `.card`, `.card__icon`, `.card__body`, `.card__title`, `.card__desc`, `.card__credit`, `.card__button` classes. The `.card` block is the unit to duplicate for future titles — Task 5 adjusts `.portfolio` grid behavior at the mobile breakpoint.

- [ ] **Step 1: Fill in portfolio markup in `index.html`**

Replace the `<section class="portfolio">` block with:

```html
    <section class="portfolio">
      <div class="card">
        <div class="card__icon" aria-hidden="true">SB</div>
        <div class="card__body">
          <h2 class="card__title">Slide Block</h2>
          <p class="card__desc">Slide, match, and clear — a colorful puzzle game.</p>
          <p class="card__credit">by LayonCraft</p>
          <!-- TODO: replace href with real Google Play store link -->
          <a class="card__button" href="#">View on Google Play</a>
        </div>
      </div>
    </section>
```

- [ ] **Step 2: Add portfolio/card styles to `style.css`**

```css
/* Portfolio */
.portfolio {
  max-width: 60rem;
  margin: 0 auto;
  padding: 2rem 1.5rem 4rem;
  display: flex;
  flex-wrap: wrap;
  gap: 1.5rem;
  justify-content: center;
}

.card {
  background: var(--bg-card);
  border-radius: 1rem;
  padding: 1.5rem;
  display: flex;
  gap: 1.25rem;
  align-items: flex-start;
  width: 100%;
  max-width: 28rem;
  transition: transform 0.2s ease, box-shadow 0.2s ease;
}

.card:hover {
  transform: translateY(-4px);
  box-shadow: 0 12px 30px rgba(255, 61, 138, 0.15);
}

.card__icon {
  flex-shrink: 0;
  width: 4rem;
  height: 4rem;
  border-radius: 0.75rem;
  background: linear-gradient(135deg, var(--primary), var(--accent));
  display: flex;
  align-items: center;
  justify-content: center;
  font-family: var(--font-heading);
  font-weight: 700;
  color: var(--text);
}

.card__title {
  font-family: var(--font-heading);
  font-weight: 700;
  font-size: 1.25rem;
  margin-bottom: 0.25rem;
}

.card__desc {
  color: var(--text-muted);
  font-size: 0.95rem;
  margin-bottom: 0.5rem;
}

.card__credit {
  color: var(--text-muted);
  font-size: 0.8rem;
  margin-bottom: 0.75rem;
}

.card__button {
  display: inline-block;
  background: linear-gradient(135deg, var(--primary), var(--accent));
  color: var(--text);
  text-decoration: none;
  font-weight: 600;
  font-size: 0.9rem;
  padding: 0.6rem 1.2rem;
  border-radius: 999px;
  transition: filter 0.2s ease;
}

.card__button:hover {
  filter: brightness(1.1);
}
```

- [ ] **Step 3: Verify in browser**

Reload `index.html`.

Expected:
- One card is visible below the hero, dark background slightly lighter than the page background.
- Card shows a gradient square icon with "SB", title "Slide Block", description, "by LayonCraft" credit line, and an orange-to-pink "View on Google Play" button.
- Hovering the card lifts it slightly with a soft pink-tinted shadow.
- Hovering the button brightens it slightly.
- View page source: the store link's `<a>` tag is preceded by an HTML comment noting it's a placeholder.

- [ ] **Step 4: Commit**

```bash
git add index.html style.css
git commit -m "Add portfolio card for Slide Block"
```

---

### Task 4: Footer section

**Files:**
- Modify: `index.html` (fill in `<footer class="site-footer">`)
- Modify: `style.css` (append footer styles)

**Interfaces:**
- Consumes: `--text-muted`, `--accent` from Task 1.
- Produces: `.site-footer`, `.footer__socials`, `.footer__social-link`, `.footer__copyright` classes.

- [ ] **Step 1: Fill in footer markup in `index.html`**

Replace the `<footer class="site-footer">` block with:

```html
  <footer class="site-footer">
    <div class="footer__socials">
      <!-- TODO: replace with real contact links -->
      <a class="footer__social-link" href="#">Email</a>
      <a class="footer__social-link" href="#">GitHub</a>
      <a class="footer__social-link" href="#">X</a>
    </div>
    <p class="footer__copyright">&copy; 2026 LayonCraft</p>
  </footer>
```

- [ ] **Step 2: Add footer styles to `style.css`**

```css
/* Footer */
.site-footer {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 0.75rem;
  padding: 2rem 1.5rem 3rem;
  text-align: center;
}

.footer__socials {
  display: flex;
  gap: 1.5rem;
}

.footer__social-link {
  color: var(--text-muted);
  text-decoration: none;
  font-size: 0.9rem;
  transition: color 0.2s ease;
}

.footer__social-link:hover {
  color: var(--accent);
}

.footer__copyright {
  color: var(--text-muted);
  font-size: 0.8rem;
}
```

- [ ] **Step 3: Verify in browser**

Reload `index.html`.

Expected:
- Footer shows three links — "Email", "GitHub", "X" — side by side, muted gray.
- Hovering a link turns it pink (`--accent`).
- Copyright line "© 2026 LayonCraft" appears centered below the links.

- [ ] **Step 4: Commit**

```bash
git add index.html style.css
git commit -m "Add footer with social placeholder links and copyright"
```

---

### Task 5: Responsive layout pass

**Files:**
- Modify: `style.css` (append media query block)

**Interfaces:**
- Consumes: `.hero`, `.hero__wordmark`, `.portfolio`, `.card` from Tasks 2–3.
- Produces: no new classes — adjusts existing ones under a `@media (max-width: 640px)` query.

- [ ] **Step 1: Add mobile breakpoint styles to `style.css`**

```css
/* Responsive */
@media (max-width: 640px) {
  .hero {
    min-height: 50vh;
    padding: 3rem 1rem;
  }

  .hero__blob {
    width: 30rem;
    height: 30rem;
  }

  .card {
    flex-direction: column;
    align-items: center;
    text-align: center;
  }

  .card__icon {
    margin-bottom: 0.5rem;
  }
}
```

- [ ] **Step 2: Verify in browser**

Open DevTools, toggle device toolbar (or resize the window) to a width under 640px (e.g. 375px, an iPhone-sized viewport).

Expected:
- Hero text remains legible and centered, no overflow or horizontal scrollbar.
- Card stacks icon above text, centered, instead of icon-beside-text.
- Resize back to a desktop width (e.g. 1280px) and confirm the desktop layout from Tasks 2–3 is unchanged.

- [ ] **Step 3: Commit**

```bash
git add style.css
git commit -m "Add mobile responsive breakpoint"
```

---

### Task 6: Scroll-reveal animation (progressive enhancement)

**Files:**
- Modify: `script.js` (full replacement of the stub)
- Modify: `style.css` (append reveal animation styles)
- Modify: `index.html` (add `reveal` class to hero and card elements)

**Interfaces:**
- Consumes: `.hero__wordmark`, `.hero__tagline`, `.card` from Tasks 2–3; the `html.js` class set in Task 1.
- Produces: `.reveal` and `.reveal.is-visible` classes; `IntersectionObserver` wiring in `script.js`.

- [ ] **Step 1: Add `reveal` class to elements in `index.html`**

Update the hero and card elements (from Tasks 2 and 3) to include the `reveal` class:

```html
    <h1 class="hero__wordmark reveal">LAYONCRAFT</h1>
    <p class="hero__tagline reveal">Crafting playful puzzle experiences.</p>
```

```html
      <div class="card reveal">
```

- [ ] **Step 2: Add reveal styles to `style.css`, scoped to JS-enabled pages only**

```css
/* Scroll reveal (progressive enhancement — only applies when JS has run) */
html.js .reveal {
  opacity: 0;
  transform: translateY(16px);
  transition: opacity 0.6s ease, transform 0.6s ease;
}

html.js .reveal.is-visible {
  opacity: 1;
  transform: translateY(0);
}
```

- [ ] **Step 3: Implement the observer in `script.js`**

```js
// script.js
const revealTargets = document.querySelectorAll('.reveal');

if ('IntersectionObserver' in window && revealTargets.length) {
  const observer = new IntersectionObserver((entries) => {
    entries.forEach((entry) => {
      if (entry.isIntersecting) {
        entry.target.classList.add('is-visible');
        observer.unobserve(entry.target);
      }
    });
  }, { threshold: 0.2 });

  revealTargets.forEach((el) => observer.observe(el));
} else {
  revealTargets.forEach((el) => el.classList.add('is-visible'));
}
```

- [ ] **Step 4: Verify in browser**

Reload `index.html` and scroll from the top.

Expected:
- On load, hero wordmark and tagline fade/slide into view shortly after the page loads (they start in view, so this should trigger almost immediately).
- Scrolling down, the portfolio card fades/slides in as it enters the viewport.
- Each element animates only once (scrolling back up and down again does not re-trigger it).

- [ ] **Step 5: Verify no-JS fallback**

In DevTools, disable JavaScript (Settings → Debugger → Disable JavaScript, or via the Command Menu "Disable JavaScript"), then reload `index.html`.

Expected:
- `<html>` no longer gets the `js` class (view page source / inspect element confirms no `class="js"` on `<html>`).
- Hero wordmark, tagline, and card are fully visible immediately, with no fade-in and no permanently-hidden content.

Re-enable JavaScript in DevTools afterward.

- [ ] **Step 6: Commit**

```bash
git add index.html style.css script.js
git commit -m "Add progressive-enhancement scroll-reveal animation"
```

# LayonCraft Studio Landing Page — Design

## Purpose

Turn the current placeholder `index.html` into a portfolio-showcase landing page for LayonCraft, an indie game/app studio. The page introduces the studio and showcases its released titles, starting with one game (Slide Block / "Color-Brick").

## Scope

- Single static page (`index.html`), no build tooling, no framework.
- Content in English only.
- One portfolio entry for now (Slide Block), built as a repeatable card structure so more entries can be added later by duplicating the card markup + data.
- Store link and social links are placeholders (`#`), to be filled in later by the user.

## File Structure

```
LayonCraft.github.io/
├── index.html      (structure + content)
├── style.css       (design system via CSS custom properties)
├── script.js       (optional: scroll-in animation via IntersectionObserver)
├── LICENSE         (unchanged)
└── app-ads.txt     (unchanged)
```

No build step. GitHub Pages serves the repo root directly.

## Content Sections

1. **Header / Hero**
   - Studio wordmark: `LAYONCRAFT`
   - One-line energetic tagline (e.g. "Crafting playful puzzle experiences.")
   - Decorative orange→pink gradient blob/shape in the background

2. **Portfolio card** (repeatable structure)
   - Game icon (placeholder square/image slot)
   - Title: "Slide Block"
   - One-line description: "Slide, match, and clear — a colorful puzzle game."
   - Credit line: "by LayonCraft"
   - "View on Google Play" button, `href="#"` placeholder, clearly marked in HTML comment for later replacement
   - Card markup structured so a second/third card can be copy-pasted with different content later

3. **Footer**
   - Social/contact links: email, GitHub, X (Twitter) — all `href="#"` placeholders
   - Copyright line: "© 2026 LayonCraft"

## Visual Design

- **Color system** (CSS custom properties):
  - `--bg`: `#0F0F14` (dark charcoal)
  - `--primary`: `#FF6B35` (orange)
  - `--accent`: `#FF3D8A` (pink/magenta)
  - `--text`: `#F5F5F5`
- **Typography**: Headline font — bold geometric sans-serif (Space Grotesk via Google Fonts, with system-font fallback). Body text — system font stack for readability.
- **Gradient accents**: orange→pink radial gradient blob behind hero content; same gradient applied to the store button background.
- **Cards**: background slightly lighter than page background; hover state lifts the card (transform + soft glow shadow).

## Responsive & Interaction

- Mobile-first layout using flexbox/grid; single breakpoint around 640px is sufficient for this content volume.
- Optional minimal JS: on-scroll fade-in/slide-up via `IntersectionObserver` for hero and card elements. Purely additive — page is fully functional without JS.
- Hover/active transitions on buttons and cards.

## Verification

No build process — verify by opening `index.html` directly in a browser:
- Check layout at desktop and mobile viewport widths.
- Confirm placeholder links (`#`) are clearly marked for later replacement.
- Confirm scroll animation triggers without errors (if implemented).

## Out of Scope

- Additional portfolio entries beyond Slide Block (structure supports adding them later, but no second entry is built now).
- Blog/news section, multi-language content, CMS/build tooling.
- Filling in real store/social links (left as placeholders per user request).

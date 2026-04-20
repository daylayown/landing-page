# CLAUDE.md — daylayown-landing-page

## What this is

Personal landing page for [daylayown.org](https://daylayown.org) by Nicholas De Leon, Senior Reporter at Consumer Reports. Clean, professional multi-page site with a warm earth-tone palette.

## Hosting

- **GitHub repo**: https://github.com/daylayown/landing-page
- **Deployed via**: GitHub Pages from `main` branch, root `/`
- **Custom domain**: `daylayown.org` (configured via `CNAME` file in repo root)
- **Push to `main`** triggers an automatic GitHub Pages rebuild
- **Analytics**: Google Analytics (`G-2V29BC0M8K`) inline in each page

## File structure

```
index.html        — Home: hero, projects, selected writing, speaking CTA, footer
speaking.html     — Speaking page: bio, talks, audiences, booking
styles.css        — Shared external stylesheet for both pages
me.jpg            — Photo used on home hero and speaking page
CNAME             — GitHub Pages custom domain (daylayown.org)
cname.txt         — Local copy of the CNAME value
```

> `index - Copy.html` is a stale backup from an earlier design iteration — safe to ignore or delete.

## Design system

Defined as CSS custom properties in `:root` (`styles.css`):

- **Palette** (warm, earth-toned):
  - `--bg: #faf8f5` (cream), `--bg-alt: #f2eeea`
  - `--text: #2b2520`, `--text-secondary: #6b5e54`
  - `--border: #e4ded7`
  - `--accent: #b45309` (copper/amber), `--accent-hover: #92400e`
  - `--accent-subtle: rgba(180, 83, 9, 0.08)`
- **Typography** (Google Fonts):
  - Body: `'DM Sans'`
  - Headings + `.nav-brand`: `'DM Serif Display'`
- **Shape**: `--radius: 6px` (round photos use `border-radius: 50%`)
- **Elevation**: `--shadow-sm / --shadow-md / --shadow-lg`
- **Layout**: `--max-width: 860px`, centered via `.container`

### Motion & interaction
- `fadeUp` keyframe on hero and sections
- Project cards lift on hover (`translateY(-2px)` + shadow + accent border)
- Nav links get an animated underline from `::after`
- Writing list items nudge right on hover
- Color/background transitions at ~0.2–0.3s

### Mobile
- Responsive breakpoint at `640px`
- Stacks hero content, switches photo to round/small, single-column audience list, centers nav

## Rules

- Keep the shared design system consistent across `index.html` and `speaking.html` — both load `styles.css`
- Preserve the warm earth-tone palette and DM Serif Display / DM Sans typography
- Don't break Google Analytics or Open Graph/Twitter meta tags
- Keep `CNAME` in place — removing it breaks the custom domain
- Maintain the footer social icons (X, LinkedIn, Instagram) as inline SVGs
- Mobile responsive behavior must still work at the 640px breakpoint
- No build tools — plain HTML/CSS only, edited directly

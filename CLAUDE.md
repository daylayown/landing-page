# CLAUDE.md — daylayown-landing-page

## What this is

Personal-professional site for [daylayown.org](https://daylayown.org) by Nicholas De Leon. It works as an ad for his expertise: a technology journalist who builds AI-powered newsrooms. One home page plus long-form essays under `/writing/<slug>/`. The speaking page was removed in November 2026 (Nicholas no longer advertises talks); it's in git history if ever needed.

## Hosting

- **GitHub repo**: https://github.com/daylayown/landing-page
- **Deployed via**: GitHub Pages from `main` branch, root `/`
- **Custom domain**: `daylayown.org` (configured via `CNAME` file in repo root)
- **Push to `main`** triggers an automatic GitHub Pages rebuild. Nothing is pushed without Nicholas's approval; preview locally first (`python3 -m http.server` from the repo root)
- **Analytics**: Google Analytics (`G-2V29BC0M8K`) inline in each page's `<head>`

## File structure

```
index.html                    — Home: hero, projects, reporting, essays, consulting callout, footer
styles.css                    — Shared stylesheet for every page (fonts load via @import here)
writing/<slug>/index.html     — Long-form essay pages, served at /writing/<slug>/
img/projects/<project>.webp   — One homepage screenshot per featured project (1440×900 capture, WebP)
me.jpg                        — Headshot; the hero's colors are sampled from it
favicon.svg / .ico            — Saguaro against a red sun, in the Big Sky palette; .ico and apple-touch-icon.png are fallbacks rendered from the SVG
CNAME                         — GitHub Pages custom domain (daylayown.org)
cname.txt                     — Local copy of the CNAME value
_drafts/                      — Local design mockups (A/B/C directions). Underscore folders aren't published by GitHub Pages; not committed
```

> `index - Copy.html` is a stale backup from an earlier design iteration — safe to ignore or delete.

## Home page content

- **Hero**: name, the line "Technology journalist. I build AI-powered newsrooms.", a short bio (factual CR employer mention), Email me / See the projects buttons.
- **Projects**, in this order (Nicholas's call): Tucson Daily Brief, The Raytrace, Local News 123, Deep Dugout, Griffey 30, Matchday Inference, Remontoir. Each has one screenshot in a navy browser frame. TDB and The Raytrace are `.project.feature` (full-width screenshot, two text columns, a `.panel`); the rest are alternating rows.
  - TDB's panel is the live AI reporter (the site's calling card), followed by a "Some of our biggest stories" row of four `.story` cards linking to tucsondailybrief.com In Depth pieces.
  - The Raytrace's panel is "What the AI editor does on its own": Claude Opus 5.5 as managing editor, which drafts requests for comment that Nicholas reviews and sends himself. Don't claim the Opus fact check holds or changes stories until `data/.factcheck-enforce` exists in that repo (it runs in shadow mode).
  - Griffey 30 (griffey30.com) is a SNES mod built with Claude Code; covered by the YouTuber SNESdrunk. Matchday Inference (matchdayinference.com) was a personalized World Cup 2026 zine that ran on OpenAI's GPT-5.5, so don't describe it as a Claude project.
  - Facts in project copy come from each project's repo (`~/claude-code-projects/tucson-daily-brief-site`, `video-game-publication`, `daily-brief-agent`, `deep-dugout`, `world-cup-project`, `remontoir`; `~/codex-projects/game-mods`) or its live site. Verify before changing numbers.
  - No "smaller projects" list (Crosswording The Situation, ESPN DTC FAQ, Reflex PS2 firmware were dropped on purpose).
- **Reporting**: six clips on a navy band. **Essays**: links to `writing/<slug>/`.
- **Consulting callout** (`.callout`, sky blue): consulting on building with AI, case by case, as long as it doesn't conflict with his ethical obligations as a journalist.

To refresh a screenshot: `chromium --headless=new --hide-scrollbars --window-size=1440,900 --virtual-time-budget=8000 --screenshot=out.png <url>`, then `magick out.png -quality 82 img/projects/<project>.webp`.

## Design system ("Big Sky")

Defined as CSS custom properties in `:root` (`styles.css`). The palette is taken from `me.jpg`.

- **Palette**:
  - `--sky: #6493bf` (the photo's sky; hero, article top bar, callout), `--sky-low: #8db3d4`
  - `--navy: #1f2645` (text, buttons, screenshot frames, Reporting band), `--navy-soft: #3a4366`
  - `--cholla: #ebe9da` (page background), `--cholla-deep: #d9d6bf`, `--card: #f6f4ea`
  - `--collar: #b3343c` (accent: links, status lines, dates), `--collar-dark: #8f2229`
- **Typography** (Google Fonts): `'Bricolage Grotesque'` for headings, nav, buttons and labels; `'Newsreader'` for body text
- **Layout**: `--wide: 1180px` via `.wrap`; essays read at `--read: 42rem`
- **Hero**: the photo fills the right ~58% and fades into the sky gradient through a CSS mask; the name is white on the sky

### Motion & interaction
- One orchestrated moment: the hero copy rises in on load (disabled under `prefers-reduced-motion`)
- Screenshots and story cards lift slightly on hover; buttons change color

### Mobile
- Breakpoints at `900px` (everything stacks to one column) and `640px` (hero photo moves below the text, brand hidden in the hero top bar, tighter padding)

### Article pages
Shell: `<header class="page-top">` (sky top bar: brand + Projects / Essays / Contact) → `<article class="article">` → `<div class="container">` → `<header class="article-header">` (H1 + `<p class="article-meta">` date) → `<div class="article-body">` → a "More essays" `.back` link → the shared footer. `.article-body` styles `<p>`, `<strong>`, `<em>`, `<a>`, `<ul>`/`<ol>` and inline `<code>`. Paths are relative (`../../`).

## Rules

- Keep the shared design system consistent across `index.html` and every `writing/<slug>/index.html`; all load `styles.css`
- Preserve the Big Sky palette and the Bricolage Grotesque / Newsreader typography
- Don't break Google Analytics or Open Graph/Twitter meta tags
- Keep `CNAME` in place: removing it breaks the custom domain
- The footer has only the LinkedIn icon, as an inline SVG (X and Instagram were removed on purpose)
- No speaking or talks content; the home page's last section is the consulting callout
- Mobile behavior must still work at the 900px and 640px breakpoints
- No build tools: plain HTML/CSS only, edited directly
- New writing samples go at `writing/<slug>/index.html`. Use short, stable, human-readable slugs: no dates, no `-v2` suffixes, no random IDs. Add an entry to the "Essays" section on the home page
- **Nothing personal may be framed as Consumer Reports content.** Nicholas is a CR Senior Reporter, but his projects, essays and consulting are personal and can't be positioned as CR-backed: no CR branding, no citing CR's methodology, testing or coverage. A factual employer mention in the bio ("Senior Reporter at Consumer Reports") and CR bylines in the Reporting clips are fine

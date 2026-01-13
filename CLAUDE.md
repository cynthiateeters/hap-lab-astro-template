# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project overview

**HAP's Learning Lab** - An Astro-based static site template for creating 6-station educational experiences. HAP (HyBit A. ProtoBot) is Prof. Teeters' apprentice who guides students through hands-on learning with his friendly first-person narrative.

This repository contains both the main project AND a `starter-template/` folder that serves as a distributable template for new labs.

## Commands

```bash
npm run dev        # Start dev server at localhost:4321
npm run build      # Production build to dist/
npm run preview    # Preview production build
```

## Architecture

### Layout system

```text
src/layouts/
├── MainLayout.astro     # Base layout with header, footer, navigation
└── StationLayout.astro  # Wraps MainLayout with station-specific props
                         # Auto-calculates prev/next navigation from stationNumber
```

Station pages pass a `stationNumber` prop (1-6) to `StationLayout`, which handles navigation links automatically.

### Component hierarchy

```text
StationLayout (stationNumber, title, subtitle, introContent, ...)
    └── MainLayout (pageTitle, navigation, footer)
        ├── Header.astro (avatar, titles)
        ├── Navigation.astro (station dots, prev/next)
        ├── <slot /> (station content)
        └── Footer.astro (copyright, reminder)
```

### Syntax highlighting

Uses Astro's built-in Shiki with `css-variables` theme, customized in `src/styles/shiki-hap-theme.css`. The `CodeBlock.astro` component wraps Astro's `<Code>` component.

Supported languages: html, css, javascript, json, markdown, bash, text, nunjucks

## Content creation workflow

1. Complete `docs/reference-cards/station-blueprint-template.md` for each station
2. Copy `src/templates/station-template.astro` to `src/pages/stations/station[N].astro`
3. Replace all `[PLACEHOLDER_*]` markers with content
4. Use `station6-template.astro` for the final station (different structure)
5. Validate with skills in `skills/` before committing
6. Run `npm run build` to verify

### Template files

| Template | Purpose |
|----------|---------|
| `src/templates/hub-template.astro` | Landing page → `src/pages/index.astro` |
| `src/templates/station-template.astro` | Stations 1-5 |
| `src/templates/station6-template.astro` | Final station (different layout) |

## HAP's voice (critical)

HAP always speaks in **first-person apprentice voice**. This is non-negotiable.

### Required patterns

- "I learned from Prof. Teeters that..."
- "When I was practicing..."
- "This was tricky for me too..."
- Share specific mistakes and what they taught

### Forbidden patterns

- "You should..." (too instructional)
- "Obviously..." or "It's simple..." (dismissive)
- "Just" or "simply" (minimizing)
- Generic statements without attribution to Prof. Teeters

See `docs/reference-cards/hap-voice-card.md` for complete guidelines.

## Characters

| Character | Role | Voice |
|-----------|------|-------|
| HAP | Narrator | First-person, curious, humble, uses 🟠 emoji |
| Prof. Teeters | Mentor | Calm, encouraging, uses analogies (max 1 appearance per station) |
| Grace Hopper | Assistant | Precise, no contractions, no emojis (only when precision matters) |

## CSS requirements

**All colors must use HSL format** - never hex or rgb:

```css
/* Correct */
--warm-orange: hsl(32, 76%, 63%);

/* Wrong */
--warm-orange: #E8A557;
```

Use "CSS custom property" terminology, never "CSS variable".

## HAP images

**Never guess image filenames.** Always verify against:
`skills/hap-image-validation/hap-cloudinary-complete-inventory.md`

Common poses:

| Filename | Use case |
|----------|----------|
| `HAP-learner_dvehmt` | Default, footer |
| `hap-laptop_xiewar` | Hero, studying |
| `hap-waving_dgzacg` | Greeting |
| `hap-broke-things_qtbum4` | Confession callouts |
| `hap-brain-explodes_wu0or8` | Breakthroughs (use sparingly!) |
| `hap-celebrating_bljvgl` | Major victories |

Cloudinary URL format:

```text
https://res.cloudinary.com/cynthia-teeters/image/upload/f_auto,q_auto,w_[WIDTH],c_limit/v[VERSION]/[FILENAME].jpg
```

## Skills for validation

Located in `skills/` directory (run with `/format skillname`):

| Skill | Purpose |
|-------|---------|
| `hap-voice` | Validate first-person apprentice voice |
| `accessibility-check` | WCAG 2.2 Level AA compliance |
| `css-standards` | HSL color format enforcement |
| `station-content` | Station structure patterns |
| `hap-image-validation` | Verify image filenames exist |

## Heading case conventions

- **HTML files**: Title Case ("What You'll Learn")
- **Markdown files**: Sentence case ("What you'll learn")

## Emoji usage

- 🟠 HAP's signature (tips, insights)
- 🔬 Science, research discoveries
- 😳 After Grace corrects HAP

Rules: Never in code blocks, never as decoration, max 2-3 per station.

## Copyright notice

All HTML files must include:

```html
<!--
HAP Educational Content © 2026 Cynthia Teeters. All rights reserved.
HyBit A. ProtoBot (HAP) character and the apprentice learning methodology are proprietary educational innovations.
-->
```

## Common pitfalls

1. **Don't copy from completed stations** - Always use templates from `src/templates/`
2. **Don't hallucinate HAP images** - Check the inventory file
3. **Don't use hex/rgb colors** - Use hsl() only
4. **Don't break HAP's voice** - First-person, humble, references mentor
5. **Don't overuse breakthrough images** - `hap-brain-explodes` max once per station
6. **Don't skip validation** - Run skills before committing

## Key documentation

| Document | Purpose |
|----------|---------|
| `docs/designing-labs/hap-narrative-and-scene-design.md` | Complete narrative framework |
| `docs/reference-cards/hap-voice-card.md` | HAP voice quick reference |
| `docs/reference-cards/station-blueprint-template.md` | Pre-writing checklist |
| `docs/reference-cards/character-quick-ref.md` | All three characters |

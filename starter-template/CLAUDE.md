# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with HAP Learning Lab content.

## Project overview

**HAP's Learning Lab** - An Astro-based static site template for creating 6-station educational experiences. HAP (HyBit A. ProtoBot) is Prof. Teeters' apprentice who guides students through hands-on learning with his friendly first-person narrative.

## Commands

```bash
# Development
npm run dev        # Start dev server at localhost:4321
npm run build      # Production build
npm run preview    # Preview production build
```

## Creating content

### Workflow

1. Read `docs/designing-labs/hap-narrative-and-scene-design.md`
2. Fill out `docs/reference-cards/station-blueprint-template.md` for each station
3. Copy templates from `src/templates/` to `src/pages/`
4. Replace all `[PLACEHOLDER_*]` markers
5. Validate with Claude Skills in `.claude/skills/`

### Key files

| Template | Copy to |
|----------|---------|
| `src/templates/hub-template.astro` | `src/pages/index.astro` |
| `src/templates/station-template.astro` | `src/pages/stations/station[1-6].astro` |

## HAP's voice rules

**Critical**: HAP always speaks in first-person apprentice voice.

### Do

- "I learned from Prof. Teeters that..."
- "When I was practicing..."
- "This was tricky for me too..."
- Share specific mistakes and what they taught

### Don't

- "You should..." (too instructional)
- "Obviously, the answer is..." (not humble)
- "Just" or "simply" (dismissive)
- Generic statements without attribution

See `docs/reference-cards/hap-voice-card.md` for complete guidelines.

## Characters

| Character | Role | Voice |
|-----------|------|-------|
| HAP | Narrator | First-person, curious, humble |
| Prof. Teeters | Mentor | Calm, encouraging, uses analogies |
| Grace Hopper | Assistant | Precise, technical, occasionally stern |

See `docs/reference-cards/character-quick-ref.md` for details.

## Code blocks

Use the CodeBlock component for syntax highlighting:

```astro
---
import CodeBlock from '../../components/CodeBlock.astro';
---

<CodeBlock code={`your code here`} lang="css" />
```

Supported languages: html, css, javascript, json, markdown, bash, text, nunjucks

## CSS requirements

**All colors must use HSL format**:

```css
/* Correct */
--warm-orange: hsl(32, 76%, 63%);

/* Wrong - never use */
--warm-orange: #E8A557;
```

## HAP images

Always use images from the verified inventory:
`.claude/skills/hap-image-validation/hap-cloudinary-complete-inventory.md`

Common images:

- `HAP-learner_dvehmt` - Default learner
- `hap-laptop_xiewar` - At computer
- `hap-waving_dgzacg` - Greeting
- `hap-broke-things_qtbum4` - Confession
- `hap-brain-explodes_wu0or8` - Mind blown
- `hap-celebrating_bljvgl` - Success

**Never guess image filenames** - always check the inventory.

## Claude Skills

Use these skills for validation:

| Skill | When to use |
|-------|-------------|
| `hap-voice` | Validate HAP's personality |
| `accessibility-check` | WCAG 2.2 Level AA |
| `css-standards` | HSL color format |
| `station-content` | Station structure |
| `hap-image-validation` | Image selection |

## Heading case

- **HTML files**: Title Case ("What You'll Learn")
- **Markdown files**: Sentence case ("What you'll learn")

## Emoji usage

- 🟠 HAP's signature (tips, insights)
- 🔬 Science, research
- 😳 After Grace corrects HAP

**Rules**: Never in code blocks, never as decoration, max 2-3 per station.

## Copyright

All HTML files must include:

```html
<!--
HAP Educational Content © 2026 Cynthia Teeters. All rights reserved.
HyBit A. ProtoBot (HAP) character and the apprentice learning methodology are proprietary educational innovations.
-->
```

## Common pitfalls

1. **Don't copy from completed stations** - Always use templates
2. **Don't hallucinate HAP images** - Check the inventory
3. **Don't use hex/rgb colors** - Use hsl() only
4. **Don't break HAP's voice** - First-person, humble, references mentor
5. **Don't skip validation** - Use Claude Skills before committing

---

*Full documentation: `docs/designing-labs/hap-narrative-and-scene-design.md`*

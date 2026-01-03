# HAP's Learning Lab Template

**Production-ready infrastructure for creating educational web learning labs**

A complete template system for building 6-station learning experiences featuring HAP (HyBit A. ProtoBot™), Prof. Teeters' apprentice who guides students through hands-on learning with his friendly first-person narrative.

---

## What is this?

This repository contains reusable infrastructure for creating HAP Learning Labs on any topic:

- **8 Claude Skills** for progressive validation
- **5 HTML/JSON templates** for stations (1-5 and 6), demos, and content
- **Static assets** (CSS, JS, data) for HAP design system
- **Zero dependencies** - pure HTML/CSS/JS, no build process
- **100% Lighthouse scores** - accessibility and performance built-in
- **Lessons learned** - documented patterns from production use

## Quick start

### 1. Copy this template

```bash
# Clone or download this repository
git clone [your-repository-url] my-new-learning-lab
cd my-new-learning-lab
```

### 2. Plan your curriculum

Open `templates/curriculum-plan-template.md` and fill in all sections:

- Learning lab theme and objectives
- 6 station topics that build progressively
- HAP's struggles and learning moments (first-person)
- Interactive demos for each station
- Code examples showing "old way" vs "what I learned"

Save as `CONTENT-PLAN.md` in your project root.

### 3. Customize the templates

**For Stations 1-5**:

```bash
# Copy the station template
cp templates/station-template.html stations/station1.html

# Fill in [PLACEHOLDER] content using your CONTENT-PLAN.md
# Maintain HAP's first-person voice
# Use Claude Skills for validation
```

**For Station 6** (AI assistance - fixed structure):

```bash
# Station 6 ALWAYS teaches AI assistance for your topic
cp templates/station6-template.html stations/station6.html

# Only customize [PLACEHOLDER] content, not the 12-section structure
```

**For interactive demos**:

```bash
# Copy the demo template
cp templates/demo-template.html demos/demo-name.html

# Customize with your demo functionality
# Follow demo-builder Skill patterns
```

**For easter egg insights**:

```bash
# Copy the easter egg template
cp templates/hybit-insights-template.json data/hybit-insights.jsonc

# Define parameters for your topic
# Write messages in HAP's voice
```

### 4. Test locally

```bash
# Start local server (required for JSON loading)
live-server --port=3000

# Test in browser
open http://localhost:3000
```

### 5. Validate with Lighthouse

```bash
# Install dependencies (one-time)
npm install

# Run Lighthouse CI on all pages
npm run lh:ci

# Target: 99+ performance, 100 accessibility
```

## What's included

### Claude Skills (`.claude/skills/`)

8 Skills that enforce HAP Learning Lab standards:

1. **hap-voice** - HAP's personality and first-person narrative
2. **accessibility-check** - WCAG 2.2 Level AA compliance
3. **security-audit** - OWASP Top 10, XSS prevention
4. **testing-framework** - Chrome DevTools / Lighthouse testing
5. **station-content** - Station HTML structure patterns
6. **demo-builder** - Interactive demo patterns
7. **css-standards** - HSL color format enforcement
8. **hap-image-validation** - HAP image verification + complete inventory

### Templates (`templates/`)

5 complete templates with [PLACEHOLDER] syntax:

1. **station-template.html** (~375 lines) - Station structure for Stations 1-5
2. **station6-template.html** (~1,041 lines) - Fixed AI assistance structure
3. **demo-template.html** (~235 lines) - Interactive demo structure
4. **curriculum-plan-template.md** (~490 lines) - Content planning guide
5. **hybit-insights-template.json** (~275 lines) - Easter egg messages

### Static assets

**CSS** (`css/`):

- `style.css` - HAP design system (~2900 lines)
- `prism-hap-theme.css` - Syntax highlighting theme

**JavaScript** (`js/`):

- `easter-egg.js` - HyBit insights system (~189 lines)

**Documentation** (`data/`):

- `README.md` - Easter egg system documentation

## Features

### Zero dependencies

- **No build process** - Edit HTML/CSS/JS directly
- **No frameworks** - Pure vanilla JavaScript
- **No npm runtime deps** - Only Lighthouse for testing
- **CDN delivery** - Images via Cloudinary
- **Progressive enhancement** - Works without JS

### Lighthouse 100s

Every page targets:

- Performance: 99-100/100
- Accessibility: 100/100
- Best Practices: 100/100
- SEO: 100/100

### HAP's apprentice voice

- First-person narrative ("I learned...")
- Shares mistakes and learning moments
- References Prof. Teeters as mentor
- Makes complex topics relatable

### Accessibility built-in

- WCAG 2.2 Level AA compliant
- Semantic HTML throughout
- Skip links for keyboard users
- ARIA labels on all interactive elements
- Contrast ratios documented

### Modern CSS patterns

- HSL color format exclusively (no hex/rgb)
- CSS custom properties for theming
- Single source of truth for colors
- BEM-inspired component naming

## Success metrics

Quality targets achieved in production (HAP's Intrinsic Layouts Learning Lab):

### Lighthouse scores

| Metric | Target | Achieved |
|--------|--------|----------|
| Performance | ≥99/100 | 99-100/100 ✅ |
| Accessibility | 100/100 | 100/100 ✅ |
| Best Practices | 100/100 | 100/100 ✅ |
| SEO | 100/100 | 100/100 ✅ |

### Validation scores

| Skill | Score | Notes |
|-------|-------|-------|
| HAP Voice | 99/100 | First-person throughout |
| Accessibility | 100/100 | WCAG 2.2 Level AA |
| CSS Standards | 99.9/100 | All hsl() format |
| Station Structure | 99.98/100 | Consistent patterns |
| Overall | 98.8/100 | Production quality |

### Time efficiency (from LESSONS-LEARNED.md)

| Optimization | Time saved per station |
|--------------|------------------------|
| Review CLAUDE.md before coding | 30 minutes |
| Write first-person from start | 20 minutes |
| Verify HAP images against inventory | 30 minutes |
| Plan 2-4 sections (not 7+) | 15 minutes |
| **Total** | **~1.5 hours** |

### Project phase efficiency

| Phase | Estimated | Actual | Savings |
|-------|-----------|--------|---------|
| Station assessment | 8-20 hrs | 5 hrs | 60-75% |
| Easter egg system | 4-5 hrs | 45 min | 85% |
| Validation | 15-21 hrs | 4 hrs | 73-81% |

Following the documented patterns results in significant time savings.

## Architecture

### File structure

```
/
├── .claude/
│   └── skills/                # 8 Claude Skills for validation
│       ├── hap-voice/
│       ├── accessibility-check/
│       ├── security-audit/
│       ├── testing-framework/
│       ├── station-content/
│       ├── demo-builder/
│       ├── css-standards/
│       └── hap-image-validation/  # Includes complete image inventory
├── templates/                 # 5 HTML/JSON/MD templates
│   ├── station-template.html      # Stations 1-5
│   ├── station6-template.html     # Station 6 (AI assistance)
│   ├── demo-template.html
│   ├── curriculum-plan-template.md
│   └── hybit-insights-template.json
├── css/                       # HAP design system
├── js/                        # Easter egg system
├── data/                      # Documentation
├── CLAUDE.md                  # Claude Code configuration
├── LESSONS-LEARNED.md         # Patterns from production use
└── README.md                  # This file
```

### Technology stack

- **HTML5** - Semantic markup
- **CSS3** - Modern features, no preprocessor
- **Vanilla JavaScript** - No jQuery, no framework
- **Native dialog element** - For easter egg modals
- **Cloudinary CDN** - Image optimization
- **Prism.js** - Syntax highlighting (optional)

## Customization workflow

### Visual workflow diagram

```
┌─────────────────────────────────────────────────────────────────────────┐
│                        HAP LEARNING LAB WORKFLOW                        │
└─────────────────────────────────────────────────────────────────────────┘

    ┌──────────────┐     ┌──────────────┐     ┌──────────────┐
    │   PLANNING   │────▶│   BUILDING   │────▶│  VALIDATING  │
    │   2-4 hrs    │     │   6-12 hrs   │     │   1-2 hrs    │
    └──────────────┘     └──────────────┘     └──────────────┘
           │                    │                    │
           ▼                    ▼                    ▼
    ┌──────────────┐     ┌──────────────┐     ┌──────────────┐
    │ • Curriculum │     │ • Stations   │     │ • 8 Skills   │
    │   plan       │     │   1-5        │     │ • Lighthouse │
    │ • 6 topics   │     │ • Station 6  │     │ • Browser    │
    │ • HAP voice  │     │ • Demos      │     │   testing    │
    │ • Demo ideas │     │ • Easter eggs│     │ • Mobile     │
    └──────────────┘     └──────────────┘     └──────────────┘
                                                     │
                                                     ▼
                                              ┌──────────────┐
                                              │  DEPLOYMENT  │
                                              │   30 min     │
                                              └──────────────┘

    CRITICAL CHECKPOINTS:
    ─────────────────────
    □ Before coding    → Review CLAUDE.md (clamp formulas, voice, colors)
    □ Before images    → Check HAP image inventory (prevent hallucination)
    □ Before commit    → Run all 8 Claude Skills
    □ Before deploy    → Lighthouse 99+/100
```

### Per-station workflow

```
┌─────────────────────────────────────────────────────────────────────────┐
│                      STATION IMPLEMENTATION (3-4 hrs)                    │
└─────────────────────────────────────────────────────────────────────────┘

    BEFORE           DURING              AFTER             READY
    ──────           ──────              ─────             ─────
    ┌─────┐         ┌─────┐             ┌─────┐          ┌─────┐
    │Read │   ───▶  │Write│   ───▶      │Valid│   ───▶   │Test │
    │Plan │         │HTML │             │Skills│         │Live │
    └─────┘         └─────┘             └─────┘          └─────┘
       │               │                   │                │
       ▼               ▼                   ▼                ▼
    • CLAUDE.md     • First-person      • css-standards   • live-server
    • Impl plan     • 2-4 sections      • hap-voice       • All pages
    • Image         • 3 insight cards   • station-content • Easter eggs
      inventory     • Verified images   • accessibility   • Mobile
                    • Proper clamp()    • hap-image       • Lighthouse
```

### Recommended process

1. **Planning phase** (2-4 hours)
   - Fill out curriculum plan template
   - Define 6 station topics
   - Write HAP's learning journey
   - Plan interactive demos

2. **Template customization** (6-12 hours)
   - Customize station HTML files (Stations 1-5 + Station 6)
   - Create interactive demos (2-3 per station)
   - Fill easter egg messages
   - Test locally

3. **Validation phase** (1-2 hours)
   - Run all 8 Claude Skills
   - Fix accessibility issues
   - Optimize performance
   - Test on mobile/tablet/desktop

4. **Deployment** (30 minutes)
   - Deploy to static host (Netlify, GitHub Pages, etc.)
   - Test in production
   - Run final Lighthouse audits

### Time estimate

**First learning lab**: 10-20 hours total (includes learning the system)
**Subsequent labs**: 6-12 hours (familiar with patterns)

See `LESSONS-LEARNED.md` for detailed time savings from following established patterns.

## Claude Skills usage

### Before writing code

Consult `css-standards` Skill - establishes color format rules

### While creating content

- `hap-voice` - Validate HAP's personality
- `station-content` - Ensure station structure
- `demo-builder` - Build interactive demos

### Before committing

- `accessibility-check` - WCAG compliance
- `security-audit` - Security patterns
- `testing-framework` - Performance tests

### How to use Skills

Claude Code automatically loads Skills from `.claude/skills/`:

1. Read the Skill's `SKILL.md` file
2. Follow progressive validation steps
3. Complete all checklists
4. Use provided code patterns

## HAP's voice guidelines

**Always use first-person apprentice voice**:

✅ "I learned from Prof. Teeters that..."
✅ "This was tricky for me too!"
✅ "Prof. Teeters showed me..."

❌ "You should learn..."
❌ "Experts recommend..."
❌ "This tutorial teaches..."

**Show vulnerability and growth**:

- Reference specific mistakes
- Share "aha!" moments
- Credit Prof. Teeters for teaching
- Make it relatable to students

See `hap-voice` Skill for complete guidelines.

## Examples

### Completed learning labs using this template

1. **Web Colors Learning Lab** - hex → color systems → harmony → accessibility → modern CSS → AI
2. *(More coming soon)*

### Station topics that work well

- Technical skills (HTML, CSS, JavaScript, accessibility)
- Design concepts (typography, layout, color theory)
- Development workflows (Git, testing, deployment)
- Tools and frameworks (any web development tool)

### Interactive demo ideas

- Calculators (contrast ratios, font sizes, grid systems)
- Converters (color formats, units, values)
- Comparisons (before/after, good/bad examples)
- Visualizers (animations, transformations, effects)
- Generators (palettes, layouts, code snippets)

## Browser support

**Minimum supported**:

- Chrome 90+
- Firefox 90+
- Safari 15.4+
- Edge 90+

**Modern features used**:

- Native `<dialog>` element
- CSS custom properties
- CSS Grid and Flexbox
- `loading="lazy"` attribute
- `fetchpriority` attribute

No polyfills required (95%+ browser coverage as of 2024).

## Deployment

### Recommended hosts

**Static site hosts** (all support this template):

- **Netlify** - Free tier, automatic HTTPS, form handling
- **GitHub Pages** - Free, integrated with GitHub repos
- **Cloudflare Pages** - Free, fast CDN, analytics
- **Vercel** - Free tier, excellent performance
- **Surge.sh** - Simple CLI deployment

### Deployment steps

1. Build is not required (static HTML/CSS/JS)
2. Upload entire directory to static host
3. Configure custom domain (optional)
4. Test all pages in production
5. Run Lighthouse audits

### GitHub Pages example

```bash
# Push to GitHub
git init
git add .
git commit -m "Initial commit"
git remote add origin [your-repo-url]
git push -u origin main

# Enable GitHub Pages in repo settings
# Select main branch, root directory
# Site will be live at https://username.github.io/repo-name
```

## Testing

### Local testing

```bash
# Start local server
live-server --port=3000

# Test all pages manually
# Test easter egg system with ?hybit= parameters
# Test on different screen sizes
```

### Lighthouse testing

```bash
# Run Lighthouse CI
npm run lh:ci

# Or test individual pages in browser
# DevTools → Lighthouse → Run audit
```

### Accessibility testing

- **Chrome DevTools** - Elements → Accessibility pane
- **WebAIM Contrast Checker** - Test all text colors
- **Screen reader** - VoiceOver (Mac) or NVDA (Windows)
- **Keyboard navigation** - Tab through entire page

### Cross-browser testing

- Test in Chrome, Firefox, Safari, Edge
- Test on mobile devices (iOS Safari, Chrome Android)
- Use DevTools device emulation
- Test with slow 3G network throttling

## Troubleshooting

### Easter egg not working

- Ensure you're using a local server (not `file://` protocol)
- Check `data/hybit-insights.jsonc` syntax (valid JSON)
- Verify parameters are in `allowedParams` array
- Test with `?hybit` (no value) for page-specific help

### Lighthouse scores below target

- Check image sizes (use explicit width/height)
- Verify `loading="lazy"` on below-fold images
- Ensure LCP image has `fetchpriority="high"`
- Remove unused CSS/JS
- Test with network throttling

### Colors showing hex codes

- Run `css-standards` Skill validation
- Search for hex codes: `grep -r '#[0-9A-Fa-f]' css/`
- Convert all hex/rgb to hsl() format
- Use CSS custom properties only

### HAP's voice sounds off

- Run `hap-voice` Skill validation
- Check for second-person ("you should...")
- Verify first-person ("I learned...")
- Add Prof. Teeters attributions
- Reference specific struggles

## Contributing

This template is production-ready and actively maintained. Contributions welcome:

1. Fork the repository
2. Create a feature branch
3. Test thoroughly with all Skills
4. Submit pull request with description

**Areas for contribution**:

- New Claude Skills
- Template improvements
- Documentation enhancements
- Example learning labs
- Bug fixes

## License

**Multi-license approach**:

- **Template code**: MIT License (free to use)
- **HAP™ character**: Proprietary (Prof. Teeters)
- **Educational methodology**: Proprietary (academic use allowed)

See individual license files for details:

- `LICENSE.md` - Template code (MIT)
- `TRADEMARK.md` - HAP™ character usage
- `CONTENT-LICENSE.md` - Educational content

**Using HAP™ character requires**:

- Attribution to Prof. Cynthia Teeters
- Maintaining trademark symbols (HAP™, HyBit A. ProtoBot™)
- Educational/non-commercial use

Commercial use requires permission. Contact: [contact information]

## Support

### Documentation

- `CLAUDE.md` - Complete Claude Code configuration
- `LESSONS-LEARNED.md` - Patterns and time savings from production use
- `data/README.md` - Easter egg system guide
- Individual Skill `SKILL.md` files - Detailed validation guides
- Template comments - Inline [PLACEHOLDER] guidance
- HAP image inventory - `.claude/skills/hap-image-validation/hap-cloudinary-complete-inventory.md`

### Getting help

- GitHub Issues - Bug reports and questions
- GitHub Discussions - Usage questions and ideas
- Documentation - Comprehensive guides included

### Updates

This template follows semantic versioning:

- **Major** - Breaking changes to structure
- **Minor** - New Skills, templates, features
- **Patch** - Bug fixes, documentation updates

## Credits

**Created by**: Prof. Cynthia Teeters
**Character design**: HAP™ (HyBit A. ProtoBot™)
**Visual elements**: Created with AI assistance
**Teaching methodology**: Apprentice learning approach

---

**Ready to create your HAP Learning Lab?**

1. Copy this repository
2. Fill out `templates/curriculum-plan-template.md`
3. Customize templates with your content
4. Validate with Claude Skills
5. Deploy and share!

Happy teaching! 🟠

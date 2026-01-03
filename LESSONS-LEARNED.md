# Lessons learned from HAP learning lab development

**Source project**: HAP's Intrinsic Layouts Learning Lab
**Compiled**: November 2025
**Purpose**: Actionable insights for creating future HAP Learning Labs

This document synthesizes lessons learned from building a complete 6-station HAP Learning Lab. Following these patterns will save significant time and prevent common mistakes.

---

## Executive summary

### Time savings from following this guide

| Lesson | Time saved per station |
|--------|------------------------|
| Review CLAUDE.md before coding | 30 minutes |
| Write in first-person from start | 20 minutes |
| Plan 2-4 sections (not 7+) | 15 minutes |
| Verify HAP images against inventory | 30 minutes |
| **Total** | **~1.5 hours per station** |

### Top 5 critical lessons

1. **Always start from templates** - Never copy from existing stations
2. **Verify HAP images before adding** - Hallucinated images are costly to fix
3. **Use computed slope formulas** - Never arbitrary percentages in clamp()
4. **Write in first-person from start** - Fixing voice violations is tedious
5. **Plan for 2-4 main sections** - Stations over 700 lines are too long

---

## Planning and preparation

### Before writing any code

**Read CLAUDE.md completely** (especially these sections):

- clamp() formula requirements
- HAP voice guidelines
- CSS color standards (hsl() only)
- HAP image inventory location

**Lesson from Station 1**: Had 8 clamp() violations because CLAUDE.md wasn't reviewed first. Cost 30 minutes to fix.

### Station structure planning

**Target metrics**:

- 600-700 lines total
- 2-4 main content sections (NOT 7+)
- EXACTLY 3 insight cards
- 2-4 HAP note callouts
- 6-8 quick reference tips

**Lesson from Station 1**: Had 7 main sections and 718 lines. Too long. Should have consolidated related topics.

### Always use templates

```bash
# CORRECT: Start from template
cp templates/station-template.html stations/station[N].html

# For Station 6 specifically
cp templates/station6-template.html stations/station6.html

# WRONG: Never do this
cp stations/station1.html stations/station2.html  # NO!
```

**Why**: Templates have CUSTOMIZE comments and consistent structure. Copying existing stations propagates mistakes.

---

## HAP voice and content

### First-person voice from the start

**Critical rule**: HAP speaks in first-person throughout. Write this way from the beginning.

**Common violations and fixes**:

| Wrong pattern | Correct pattern |
|---------------|-----------------|
| "helps you see" | "helped me see" |
| "let you define" | "define" (neutral) or "let me define" |
| "As you drag" | "When I drag" |
| "your project" | "my project" or "a project" |
| "you'll learn" | neutral description |

**Acceptable exceptions**:

- Prof. Teeters quotes: "HAP, you need to use computed slopes"
- Forward references: "we'll explore in Station 5" (minor, acceptable)

**Lesson from Station 1**: Had 7 voice violations. Each one required reading context and careful editing. Prevention is 5x faster than fixing.

### HAP's narrative structure

**Every station should include**:

1. **HAP's struggle/mistake** - What HAP did wrong initially
2. **Prof. Teeters intervention** - What Prof. Teeters asked/taught
3. **HAP's aha moment** - The breakthrough realization
4. **Practical application** - How HAP now does it correctly

**Example pattern** (from Station 3):
> "I tried `clamp(1rem, 5%, 3rem)` because 5% seemed reasonable! Wrong! Prof. Teeters explained: 'HAP, that 5% is relative to the parent element's width, not the viewport!'"

### Insight cards rules

**EXACTLY 3 cards** - No more, no less

**Structure per card**:

```html
<div class="insight-card">
    <h3><span class="insight-icon">[EMOJI]</span> [Title]</h3>
    <p class="stat-large">[Key concept]</p>
    <p>[HAP's first-person explanation]</p>
</div>
```

**Stat variations**: `stat-large`, `stat-teal`, `stat-brown`

---

## HAP image management

### Critical: Prevent hallucinated images

**Problem discovered**: AI frequently invents HAP image filenames that don't exist. Station 2 had 5 out of 6 HAP images hallucinated. Cost 30 minutes to fix.

**Solution**: Always verify against inventory BEFORE adding any HAP image.

**Inventory location**: `.claude/skills/hap-image-validation/hap-cloudinary-complete-inventory.md`

### Workflow for adding HAP images

1. **Identify emotional context** of the content
2. **Open inventory file** and find matching category
3. **Copy exact filename** (e.g., `hap-confused-map_q8q0ej`)
4. **Copy exact version number** (e.g., `v1759495999`)
5. **Use recommended alt text** from inventory
6. **Verify URL is correct** before saving

### Emotional journey per station

**Recommended image progression**:

| Position | Image category | Example |
|----------|---------------|---------|
| Hero | Neutral studying | `hap-laptop_xiewar` |
| Mistake | Confusion/struggle | `hap-confused-map_q8q0ej` |
| Breakthrough | Major realization | `hap-brain-explodes_wu0or8` (MAX 1) |
| Understanding | Confidence | `hap-thumbs-up_s4si0j` |
| Practice | Reflection | `HAP-learner_dvehmt` (2-3x) |
| Footer | Reflection | `HAP-learner_dvehmt` |

**Critical constraint**: Use `hap-brain-explodes` maximum ONCE per station (reserved for biggest breakthrough).

## CSS standards

### clamp() formula requirements

**Critical rule**: Always use computed slope formula, never arbitrary percentages.

**Formula**: `clamp(min, base + slope × viewport-unit, max)`

Where:

- `slope = (max-size - min-size) ÷ (max-viewport - min-viewport)`
- `base = min-size - (slope × min-viewport)`

**Examples**:

```css
/* CORRECT - computed slope */
padding: clamp(1rem, 0.5rem + 1vw, 3rem);
gap: clamp(0.5rem, 0.4rem + 0.5vw, 1rem);

/* WRONG - arbitrary percentage */
padding: clamp(1rem, 5%, 3rem);  /* 5% is unpredictable! */

/* WRONG - viewport unit alone (no base) */
padding: clamp(1rem, 2vw, 3rem);  /* Missing base calculation */
```

**Lesson from Station 1**: Had 8 clamp() violations, all using arbitrary percentages. Every single one had to be recalculated with proper slope formula.

### Color format enforcement

**Rule**: All colors MUST use hsl() format

**Validation from production**: Zero hex or rgb colors in final codebase. 3 instances of old `hsla()` syntax found (minor, but prefer modern `hsl()` with alpha channel).

### CSS custom properties

**All colors defined in `:root`** - single source of truth

**Usage**: Always reference via `var(--custom-property)`, never repeat raw hsl() values.

---

## Demo patterns

### Pure CSS demos preferred

**Lesson learned**: Pure CSS demos are simpler and more reliable than JavaScript-based demos.

**Demo count by station**:

| Station | Demos | Type | Major concepts |
|---------|-------|------|----------------|
| Station 1 | 1 | JavaScript | Viewport simulation (necessary) |
| Station 2 | 1 | Pure CSS | Content-sizing keywords |
| Station 3 | 2 | Pure CSS | Clamp formula, :has() |
| Station 4 | 2 | Pure CSS | Magic pattern, auto-fit/fill |
| Station 5 | 1 | Standalone | Container queries |
| Station 6 | 1 | Pure CSS | AI drift comparison |

**Pattern**: 1 demo per major concept. Use JavaScript only when necessary (viewport simulation).

### Side-by-side comparison pattern

**Most effective demo pattern**: Show WRONG vs RIGHT side by side.

```html
<div class="warning-box">
    <h3>HAP's Old Way vs. What I Learned</h3>
    <p><strong class="text-error">WRONG: [What HAP did]</strong></p>
    <pre><code class="language-css">[Bad code]</code></pre>

    <p><strong class="text-success">RIGHT: What I Learned</strong></p>
    <pre><code class="language-css">[Good code]</code></pre>
</div>
```

**Color coding**: Use `text-error` (red) for wrong, `text-success` (green) for correct.

---

## Validation process

### Run all 8 Skills in order

1. **css-standards** (5 min) - Color format, custom properties
2. **hap-voice** (10 min) - First-person validation
3. **station-content** (5 min) - Structure, insight cards
4. **accessibility-check** (5 min) - WCAG AA compliance
5. **security-audit** (3 min) - XSS prevention
6. **testing-framework** (2 min) - Test plan creation
7. **hap-image-validation** (5 min) - Image verification
8. **demo-builder** (if demos present) - Demo validation

**Total validation time**: ~35 minutes per station

### Common validation findings

**From Phase 4 validation of 7 pages**:

| Skill | Score | Issues found |
|-------|-------|--------------|
| HAP Voice | 99/100 | 7 minor "you should" instances |
| Accessibility | 100/100 | Zero issues |
| CSS Standards | 99.9/100 | 3 old hsla() syntax, 6 clamp() without base |
| Station Structure | 99.98/100 | 1 aria-label naming inconsistency |

**Key insight**: Most issues are minor. The validation process catches them early, preventing user-facing problems.

---

## Station 6 specifics

### Fixed structure (non-negotiable)

Station 6 ALWAYS teaches AI assistance and follows a fixed 12-section structure:

1. What You'll Learn (3 insight cards + HAP's confession)
2. What AI Can and Can't Do
3. [First Specific Topic Example with AI]
4. [Second Specific Topic Example with AI]
5. AI for [Topic] Accessibility
6. Optimizing [Topic] Performance with AI
7. Try It Yourself: AI [Topic] Challenge
8. HAP's Rules for Working with AI (6 numbered rules)
9. Advanced Prompt Strategies
10. When NOT to Use AI
11. Quick Reference: AI [Topic] Tasks
12. Learning Objectives Checklist

**Template**: Use `templates/station6-template.html` (1,041 lines)

**Customization**: Only customize [PLACEHOLDER] content, not structure.

---

## Easter egg system

### Quick setup (45 minutes)

**Lesson learned**: Phase 3 took 45 minutes instead of estimated 4-5 hours by following clear patterns.

**Structure**: 20 parameters total

- 2 global (`detail`, `stations`)
- 18 station-specific (3 per station)

**Naming convention**: kebab-case (`station3-slope`, `station5-cqi`)

### Message quality patterns

**Good message structure**:

```json
{
  "title": "[EMOJI] [3-8 word title]",
  "content": "[2-5 sentences with HAP's voice, <code>/<strong>/<em> tags]"
}
```

**Critical concept emphasis** (example from Station 3):
> "**This was THE critical lesson!** Prof. Teeters said: *'Never use `clamp(1rem, 5%, 3rem)`—that 5% is unpredictable!'*"

---

## Performance optimization

### Image optimization checklist

- [ ] HAP avatar has `fetchpriority="high"` (LCP optimization)
- [ ] All images have explicit `width` and `height` (prevents CLS)
- [ ] Below-fold images have `loading="lazy"`
- [ ] All images have `decoding="async"`
- [ ] Cloudinary URLs use `f_auto,q_auto` for format optimization

### Font optimization

- Variable fonts (single file vs multiple weights)
- WOFF2 format (best compression)
- `font-display: swap` (prevents FOIT)
- Preloading critical fonts

---

## Time efficiency insights

### Phase-by-phase actual vs estimated

| Phase | Estimated | Actual | Savings |
|-------|-----------|--------|---------|
| Phase 1 (Station assessment) | 8-20 hours | 5 hours | 16-28 hours |
| Phase 2 (Hub page) | 3-4 hours | 2 hours | 1-2 hours |
| Phase 3 (Easter eggs) | 4-5 hours | 45 min | 3.5-4.5 hours |
| Phase 4 (Validation) | 15-21 hours | 4 hours | 11-17 hours |
| Phase 5 (Polish) | 9-14 hours | 2 hours | 7-12 hours |

**Total savings**: 38-64 hours (from following established patterns)

### Why assessments were faster than building

**Key insight**: All 6 stations were already complete when Phase 1 assessed them. The assessment phase discovered that no new demos were needed.

**Pattern for future projects**: Assess existing work thoroughly before creating new content. You may already have everything you need.

---

## Workflow summary

### Before each station

1. Read implementation plan completely
2. Review CLAUDE.md (clamp(), voice, colors)
3. Open HAP image inventory
4. Set up todo list with 7-8 tasks
5. Estimate 600-700 lines, 2-4 sections

### During implementation

1. Always start from template (never copy stations)
2. Write in first-person (HAP's voice) from the start
3. Verify each HAP image against inventory
4. Use computed slope formulas in clamp()
5. Add EXACTLY 3 insight cards
6. Include 2-4 HAP note callouts

### After implementation

1. Run all 8 Skills in order
2. Fix voice violations (P0 → P1 → P2)
3. Fix clamp() violations if any
4. Verify all fixes with grep
5. Check line count (consolidate if > 700)
6. Create validation summary
7. Test locally with live-server

---

## Common mistakes to avoid

### Critical mistakes (high impact)

1. **Copying from existing stations** instead of templates
2. **Hallucinating HAP images** without checking inventory
3. **Using arbitrary percentages** in clamp() formulas
4. **Writing in second-person** then fixing later
5. **Creating 7+ sections** causing bloated stations

### Minor mistakes (low impact)

1. Using old `hsla()` syntax instead of modern `hsl()`
2. "we'll" in forward references (acceptable but not ideal)
3. Missing `fetchpriority="high"` on hero images
4. Forgetting `loading="lazy"` on below-fold images

---

## Conclusion

Following these lessons learned will result in:

- **~1.5 hours saved per station** (7.5 hours across 5 stations)
- **Higher first-pass validation scores** (95-100 instead of 85-90)
- **Consistent quality** across all stations
- **Fewer tedious fix cycles**

The most impactful changes:

1. **Review CLAUDE.md before coding** (prevents clamp() violations)
2. **Verify HAP images against inventory** (prevents hallucination)
3. **Write first-person from start** (prevents voice violations)

**Remember**: Prevention is always faster than fixing. The extra 15 minutes of preparation saves 1.5 hours of fixes.

---

**Document version**: 1.0
**Based on**: HAP's Intrinsic Layouts Learning Lab (6 stations, 8 pages, ~14,000 lines)
**Quality achieved**: 98.8/100 overall score

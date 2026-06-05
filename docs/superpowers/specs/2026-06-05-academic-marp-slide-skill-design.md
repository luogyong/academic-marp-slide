# Academic Marp Slide Skill — Design Spec

**Date:** 2026-06-05
**Status:** Approved → Implementation
**Source:** Based on [academic-pptx-skill](https://github.com/Gabberflast/academic-pptx-skill) by Gabberflast

## Goal

Create a Claude Code skill that generates **Marp markdown** academic presentations using the neobeam-lgy theme ecosystem. Additionally, generate 3 new Marp CSS themes adapted from the slide_patterns.md design philosophy.

## Architecture

```
Marp-theme-for-academic/
├── SKILL.md                     # Skill entry point (NEW)
├── content_guidelines.md        # Academic content guidelines, Marp-adapted (NEW)
├── slide_patterns_marp.md       # Marp-specific slide pattern reference (NEW)
├── css/
│   ├── neobeam-lgy.css          # Existing rich academic theme
│   ├── academic-minimal.css     # NEW: 极简学术风
│   ├── academic-fusion.css      # NEW: 融合风格
│   └── academic-full.css        # NEW: 完整slide patterns移植
├── readme.md                    # Updated
└── marp_snippets.code-snippets  # Updated
```

## Three CSS Themes

### 1. academic-minimal.css — 极简学术风
Strict adherence to slide_patterns.md design philosophy:
- White background (`#FFFFFF`), no gradients
- Two-color palette: navy `#1F4E79` (primary) + mid-blue `#2E75B6` (accent)
- Single font: Arial / Calibri / Helvetica
- Left-aligned grid layout, consistent margins (0.5" minimum)
- Action titles: 24-28pt bold, complete sentence, thin rule divider underneath
- No decorative elements, no icon circles, no accent lines
- Body text: 20pt minimum
- Table: minimal horizontal rules only
- Blockquote: simple left-border accent
- Section divider: dark navy background slide
- Conclusions: dark background mirroring title slide

### 2. academic-fusion.css — 融合风格
Neobeam design assets + slide_patterns minimal palette:
- White background, optional subtle top-tint fade (from neobeam)
- Neobeam color system but desaturated: navy primary, steel blue accent
- Inter font + Chinese font stack (keep neobeam typography)
- Neobeam-style header bar (simplified, lighter)
- Keep neobeam .box / .beamer but limited to 3 color variants
- Neobeam table styles with single-color header
- Neobeam section divider (gradient) with slide_patterns typography
- Columns system from neobeam preserved

### 3. academic-full.css — 完整移植
All 10 slide patterns from slide_patterns.md as Marp CSS classes:
- `.slide-title` — Dark navy title slide
- `.slide-motivation` — Two-column context+gap layout
- `.slide-research-question` — Prominent callout box for RQ
- `.slide-methods` — Two-column design+variables
- `.slide-results` — Figure-left + interpretation-right
- `.slide-discussion` — Interpretation + limitation sections
- `.slide-conclusions` — Dark background takeaway slide
- `.slide-section` — Section divider with number
- `.breadcrumb` — Optional persistent navigation bar
- `.slide-references` — Reference list styling
- `.slide-appendix` — Muted-label appendix slides

## Skill Workflow (SKILL.md)

Same 4-step flow as academic-pptx-skill:

1. **Identify Presentation Type** — Structured Argument (default) vs Visual/Narrative
2. **Plan Deck** — Slide-by-slide outline with action titles, ghost deck test
3. **Apply Design Standards** — Theme selection, Marp-specific formatting
4. **Build and QA** — Generate Marp MD, run academic QA checklist

### Theme Selection Logic
- Default: `neobeam-lgy` (richest features, best for Chinese academic)
- When user wants minimal/high-impact: `academic-minimal`
- When user wants blend: `academic-fusion`
- When user wants full slide pattern control: `academic-full`

### Marp-Specific Adaptations
- `<!-- _class: X -->` for per-slide styling
- HTML `<div class="...">` for boxes, columns, beamer blocks
- `![#center](./figure.png)` for image positioning
- `$$...$$` for math (KaTeX)
- Front matter: `marp: true, theme: X, paginate: true, math: katex, size: 16:9`

## Key Principles (inherited from academic-pptx-skill)

1. Action titles, not topic labels
2. One argument, made well
3. One insight per slide
4. Slides support speech; they don't replace it
5. Cite everything borrowed
6. End on conclusions

## Dependencies

- None (pure Marp markdown output)
- VS Code: Marp for VS Code extension (for preview)
- CLI: @marp-team/marp-cli (for export)
- No Python, no Node.js runtime dependency for skill itself

---
name: academic-marp-slide
description: "Create academic presentations as Marp markdown with neobeam-lgy theme ecosystem. Use when the user wants conference talks, seminar slides, thesis defenses, grant briefings, lab meetings, or any academic presentation as Marp markdown. Triggers: 'conference talk', 'seminar slides', 'thesis defense', 'research presentation', 'academic deck', 'make slides for my paper', 'Marp presentation', 'academic marp'. This skill governs CONTENT and STRUCTURE. For the CSS themes, see css/ directory."
license: MIT
---

# Academic Marp Slide Skill

Generate academic presentations as **Marp markdown** — enforced action titles, structured argument, communication-first design. Powered by the neobeam-lgy theme ecosystem.

## How This Skill Works

1. **SKILL.md** (this file) — content strategy, argument structure, design standards, theme selection
2. **[content_guidelines.md](content_guidelines.md)** — detailed academic writing rules adapted for Marp
3. **[slide_patterns_marp.md](slide_patterns_marp.md)** — per-slide-type Marp patterns

Output is **Marp markdown** (`.md`), rendered with one of four CSS themes in `css/`.

---

## Theme Selection

Four themes available — choose based on the presentation context:

| Theme | CSS File | Style | Best For |
|-------|----------|-------|----------|
| **neobeam-lgy** | `neobeam-lgy.css` | Rich academic (gradients, multi-color boxes, beamer blocks) | Chinese academic, course lectures, comprehensive talks |
| **academic-minimal** | `academic-minimal.css` | Minimalist (white bg, navy+blue, single font, no decoration) | High-impact conference talks, strict slide_patterns.md |
| **academic-fusion** | `academic-fusion.css` | Blend (neobeam components + minimal palette) | Balanced academic presentations |
| **academic-full** | `academic-full.css` | Full slide patterns (all 10 patterns as CSS classes) | Complex decks needing explicit pattern control |

### Default Theme Logic

- **Chinese content or teaching**: default to `neobeam-lgy` (richest features, CJK font stack)
- **English conference talk**: default to `academic-minimal` (slide_patterns.md philosophy)
- **User preference unclear**: ask, showing the table above

---

## Step 1: Identify Presentation Type

Before planning a single slide, determine which mode applies.

### Structured Argument (default for academic work)

Use for: conference papers, seminar talks, thesis defenses, dissertation chapters, grant briefings, lab presentations.

**Priority: argument structure → data → layout → aesthetics.**

Follow [content_guidelines.md](content_guidelines.md) in full.

### Visual / Narrative

Use for: public engagement talks, lay panels, event keynotes, science communication.

Argument structure still matters, but visual storytelling takes priority.

### When in doubt

Default to **Structured Argument**. If the user mentions a paper, study, dataset, thesis, or grant → Structured Argument.

---

## Step 2: Plan the Deck Before Writing Any Slides

Produce a slide-by-slide outline and confirm with the user if the deck is > 10 slides.

**Ghost deck test**: read only the action titles in sequence. They must tell the complete argument. If they don't, fix the outline before writing.

---

## Step 3: Generate Marp Markdown

### Front Matter Template

```yaml
---
marp: true
theme: neobeam-lgy     # or: academic-minimal, academic-fusion, academic-full
paginate: true
math: katex
size: 16:9
footer: '<span>Author / Institution</span><span>Presentation Title</span><span>Date</span>'
---
```

### Slide Type Markers

| Slide Type | Marp Directive | Theme Support |
|------------|---------------|---------------|
| Title slide | `<!-- _class: title -->` | neobeam-lgy, academic-minimal |
| Section divider | `<!-- _class: section -->` | neobeam-lgy, academic-fusion |
| Content (default) | (none needed) | All themes |
| Conclusions | `<!-- _class: conclusions -->` | academic-minimal, academic-fusion |
| Results layout | `<!-- _class: results -->` | academic-full |
| Discussion | `<!-- _class: discussion -->` | academic-full |
| References | `<!-- _class: references -->` | All themes |
| Appendix | `<!-- _class: appendix -->` | academic-minimal, academic-full |
| Dark variant | `<!-- _class: dark -->` | neobeam-lgy |

### Key Components (Marp Syntax)

**Action titles** — every content slide h1 is a complete sentence:
```markdown
# Treatment effect is significant across all three cohorts
```

**Two-column layout**:
```html
<div class="columns-6-4">
<div>

### Left column
Content here

</div>
<div>

### Right column
Content here

</div>
</div>
```

**Info boxes** (neobeam-lgy, academic-fusion, academic-full):
```html
<div class="box info" data-label="Key Finding">
Significant effect at p < 0.001
</div>
```

**Beamer blocks**:
```html
<div class="beamer theme" data-label="Takeaway">
Main conclusion here
</div>
```

**Results slide pattern** (academic-full):
```html
<div class="columns-6-4">
<div>

![#center](./result.png)
###### Figure 1: Main result

</div>
<div>

### What to take away
- Key finding 1
- Key finding 2

</div>
</div>
```

**Citations**:
```html
<div class="cite">
Author et al. (2024), Journal Name
</div>
```

**Research question callout** (academic-full, academic-minimal):
```html
<div class="callout">
Do effects of the X program on cognitive skills persist to age 35?
</div>
```

---

## Step 4: Theme-Specific Patterns

### When using neobeam-lgy.css

- Use `<!-- _class: title -->` for cover, `<!-- _class: section theme-* -->` for chapters
- Full `.box` color palette (info, success, warn, alert, theorem + 20+ colors)
- Full `.beamer` color variants (theme, example, warn, navy, purple, teal, etc.)
- Use `.formula-box` for key equations
- `.dense` / `.denser` / `.densest` for content-heavy slides
- `.wide` for wide tables
- `<!-- _class: dark -->` for emphasis slides

### When using academic-minimal.css

- White backgrounds only — let content breathe
- Action titles with thin rule dividers (automatic)
- Minimal color: navy titles, blue accents only
- No boxes by default — use blockquote `> #### Label` for labeled content
- `.callout` for research questions, `.limitation` for caveats
- Clean tables with horizontal rules only

### When using academic-fusion.css

- Neobeam layout + simplified palette
- `.box` with 3 color variants (note, success, warn)
- `.beamer` with 3 color variants (theme, example, warn)
- Neobeam-style header bar and footer
- Gradient section dividers

### When using academic-full.css

- Rich class system: `.slide-title`, `.slide-motivation`, `.slide-research-question`,
  `.slide-methods`, `.slide-results`, `.slide-discussion`, `.slide-conclusions`,
  `.slide-section`, `.slide-references`, `.slide-appendix`
- `.breadcrumb-bar` for long presentations
- `.finding-callout` for chart annotations
- `.section-label` for within-slide section headers
- `.limitation-block`, `.contact` for discussion/conclusions slides

---

## Step 5: Academic QA Checklist

Run after generating the Marp file:

```
Academic QA checklist:
□ Every content slide has an action title (complete sentence stating the takeaway)
□ Ghost deck test passes (action titles alone tell the full argument)
□ One exhibit per results slide; each exhibit has a "so what" annotation
□ Every borrowed figure or data point has an in-slide citation
□ A References slide exists at the end
□ Conclusions slide is the last main slide (not "Thank You" or blank)
□ Contact information on the final slide
□ Font sizes are readable (≥ 20 pt body text in minimal themes)
□ No decorative elements that don't carry content
□ Section dividers present for decks > 15 slides
□ Marp front matter correct (theme name matches CSS file)
□ Theme CSS file path correctly configured in VS Code settings
```

---

## Key Principles

1. **Action titles, not topic labels.** Every slide title is a complete sentence. Reading titles alone tells the whole argument.
2. **One argument, made well.** Pick the claim that fits the time. Everything else → appendix.
3. **One insight per slide.** One exhibit per results slide. Annotate the key finding.
4. **Slides support speech; they don't replace it.** Body text orients; the presenter argues.
5. **Cite everything borrowed.** In-slide citation + References slide.
6. **End on conclusions.** Conclusions slide stays on screen during Q&A.

---

## Exporting

### VS Code (Marp for VS Code extension)
1. Open the `.md` file
2. `Ctrl+Shift+P` → `Marp: Export Slide Deck`
3. Choose format (PDF, PPTX, HTML)

### CLI
```bash
# Install
npm install -g @marp-team/marp-cli

# Export with specific theme
marp slides.md --theme css/neobeam-lgy.css --pdf
marp slides.md --theme css/academic-minimal.css --pdf
```

### Theme Configuration (VS Code settings.json)
```json
{
  "markdown.marp.themes": [
    "./css/neobeam-lgy.css",
    "./css/academic-minimal.css",
    "./css/academic-fusion.css",
    "./css/academic-full.css"
  ]
}
```

---

## Dependencies

- **Zero runtime dependencies** — pure Marp markdown output
- Recommended: [Marp for VS Code](https://marketplace.visualstudio.com/items?itemName=marp-team.marp-vscode) for preview
- Optional: `@marp-team/marp-cli` for CLI export

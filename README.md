# Academic Marp Slide Skill

A Claude Code skill for creating academic presentations as **Marp markdown**. Enforces action titles, structured argument, exhibit discipline, citation standards, and communication-first design.

Based on [academic-pptx-skill](https://github.com/Gabberflast/academic-pptx-skill) by Gabberflast — adapted for Marp output.

## Installation

### 1. Clone the Skill

Clone this repo into your Claude Code skills directory:

```bash
# Create skills directory if it doesn't exist
mkdir -p ~/.claude/skills

# Clone the skill
git clone https://github.com/luogyong/academic-marp-slide.git ~/.claude/skills/academic-marp-slide
```

Or clone anywhere and register the path in Claude Code settings (`~/.claude/settings.json`):

```json
{
  "skills": {
    "additionalPaths": ["F:/path/to/academic-marp-slide"]
  }
}
```

### 2. Install the neobeam-lgy Theme (Recommended)

The richest theme depends on [neobeam-lgy](https://github.com/luogyong/Marp-theme-for-academic):

```bash
# Clone alongside
git clone https://github.com/luogyong/Marp-theme-for-academic.git ~/marp-themes/Marp-theme-for-academic
```

### 3. Configure VS Code for Marp

Install [Marp for VS Code](https://marketplace.visualstudio.com/items?itemName=marp-team.marp-vscode), then add all theme paths to `settings.json`:

```json
{
  "markdown.marp.themes": [
    "~/marp-themes/Marp-theme-for-academic/css/neobeam-lgy.css",
    "~/.claude/skills/academic-marp-slide/css/academic-minimal.css",
    "~/.claude/skills/academic-marp-slide/css/academic-fusion.css",
    "~/.claude/skills/academic-marp-slide/css/academic-full.css"
  ]
}
```

### 4. Verify Installation

Restart Claude Code (or VS Code), then type:

> "Use academic-marp-slide to make a test slide"

Or invoke directly: `/academic-marp-slide`

## Quick Start

Once installed, just describe what you need:

> "Make slides for my paper on early childhood intervention"
> "Create a conference talk for my ACL submission"
> "Build a thesis defense presentation"

The skill will plan your deck, generate Marp markdown, and apply the right theme automatically.

## What This Skill Does

1. **Extracts** — For PDF inputs, calls MinerU Open API to extract full text + all figures to `.md` (saved next to the source PDF)
2. **Plans** — Identifies presentation type, builds slide-by-slide outline with action titles and figure assignment
3. **Generates** — Produces Marp markdown (`.md`) with proper theme, layout, components, and in-body figures
4. **Appends** — Adds an image appendix at the end: one slide per figure from the paper, with captions
5. **QA's** — Runs academic checklist: ghost deck test, citation check, figure coverage, appendix completeness

## Themes

Four Marp CSS themes available:

| Theme | CSS File | Style |
| ----- | -------- | ----- |
| **neobeam-lgy** | [neobeam-lgy.css](https://github.com/luogyong/Marp-theme-for-academic) | Rich academic (gradients, multi-color boxes, beamer blocks, CJK fonts) |
| **academic-minimal** | [css/academic-minimal.css](css/academic-minimal.css) | Minimalist (white bg, navy+blue, single font, no decoration) |
| **academic-fusion** | [css/academic-fusion.css](css/academic-fusion.css) | Blend (neobeam components + minimal palette) |
| **academic-full** | [css/academic-full.css](css/academic-full.css) | Full pattern library (10 slide pattern CSS classes) |

## Files

```text
academic-marp-slide/
├── SKILL.md                     # Skill entry point — workflow, theme selection, Marp syntax
├── content_guidelines.md        # Academic content rules (action titles, argument, citations)
├── slide_patterns_marp.md       # Per-slide-type Marp patterns + component cheat sheet
├── css/
│   ├── academic-minimal.css     # Minimal academic theme
│   ├── academic-fusion.css      # Fusion theme (neobeam + minimal)
│   └── academic-full.css        # Full slide pattern theme
├── docs/superpowers/specs/      # Design spec
└── README.md
```

## CLI Export

```bash
npm install -g @marp-team/marp-cli
marp slides.md --theme css/academic-minimal.css --pdf
marp slides.md --theme css/academic-minimal.css --pptx
```

## Key Principles

1. **Action titles, not topic labels** — Every slide title is a complete sentence. Ghost deck test: titles alone tell the whole argument.
2. **One argument, made well** — Pick the claim that fits the time. Everything else → appendix.
3. **One insight per slide** — One exhibit per results slide. Annotate the key finding.
4. **Slides support speech; they don't replace it** — Body text orients; the presenter argues.
5. **Cite everything borrowed** — In-slide citation + References slide.
6. **End on conclusions** — Conclusions slide stays on screen during Q&A.

## Dependencies

- **Zero runtime dependencies** — pure Marp markdown output
- Recommended: Marp for VS Code (preview)
- Optional: `@marp-team/marp-cli` (export)

## Credits

- Content methodology adapted from [Gabberflast/academic-pptx-skill](https://github.com/Gabberflast/academic-pptx-skill)
- neobeam-lgy theme from [luogyong/Marp-theme-for-academic](https://github.com/luogyong/Marp-theme-for-academic)
- Built on [Marp](https://marp.app/) — Markdown Presentation Ecosystem

## License

MIT

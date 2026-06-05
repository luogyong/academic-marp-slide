# Academic Marp Slide Skill

A Claude Code skill for creating academic presentations as **Marp markdown**. Enforces action titles, structured argument, exhibit discipline, citation standards, and communication-first design.

Based on [academic-pptx-skill](https://github.com/Gabberflast/academic-pptx-skill) by Gabberflast — adapted for Marp output.

## Quick Start

In Claude Code, invoke the skill when you need academic slides:

> "Make slides for my paper on early childhood intervention"
> "Create a conference talk for my ACL submission"
> "Build a thesis defense presentation"

## What This Skill Does

1. **Plans** — Identifies presentation type, builds slide-by-slide outline with action titles
2. **Generates** — Produces Marp markdown (`.md`) with proper theme, layout, and components
3. **QA's** — Runs academic checklist: ghost deck test, citation check, font sizes, etc.

## Themes

Four Marp CSS themes available:

| Theme | CSS File | Style |
|-------|----------|-------|
| **neobeam-lgy** | [neobeam-lgy.css](https://github.com/luogyong/Marp-theme-for-academic) | Rich academic (gradients, multi-color boxes, beamer blocks, CJK fonts) |
| **academic-minimal** | [css/academic-minimal.css](css/academic-minimal.css) | Minimalist (white bg, navy+blue, single font, no decoration) |
| **academic-fusion** | [css/academic-fusion.css](css/academic-fusion.css) | Blend (neobeam components + minimal palette) |
| **academic-full** | [css/academic-full.css](css/academic-full.css) | Full pattern library (10 slide pattern CSS classes) |

## Files

```
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

## VS Code Setup

Install [Marp for VS Code](https://marketplace.visualstudio.com/items?itemName=marp-team.marp-vscode), then add theme paths to `settings.json`:

```json
{
  "markdown.marp.themes": [
    "./css/academic-minimal.css",
    "./css/academic-fusion.css",
    "./css/academic-full.css",
    "./neobeam-lgy.css"
  ]
}
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

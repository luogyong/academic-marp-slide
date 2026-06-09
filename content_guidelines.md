# Academic Presentation Content Guidelines (Marp Edition)

Adapted from Gabberflast/academic-pptx-skill for Marp markdown output.

## 1. Argument Structure

### Lead with the research question
State the central question explicitly — in slides 2 or 3 at the latest.

### Use a proven narrative spine

**Option A — Situation / Complication / Resolution (SCR)**
- Situation: what was known
- Complication: what was missing or contested
- Resolution: what your work contributes

**Option B — Funnel + Answer**
- Broad context → specific gap → your approach → key findings → implications

**Option C — Answer First** (for senior/time-pressured audiences)
- Lead with the conclusion, then support it

### One argument per presentation
Choose the claim that fits the time. Everything else → appendix.

### Each slide has one job
If a slide does two things, split it.

### Flow test
After outlining, read slide titles in order. Each should make the next feel natural.

---

## 2. Action Titles

Every content slide title must be a complete sentence stating the takeaway.

| Instead of (topic label) | Use (action title) |
|--------------------------|-------------------|
| Results | Treatment effect is significant across all three cohorts |
| Literature Review | Prior work leaves the causal mechanism unexplained |
| Data | Dataset covers 40 years of county-level panel data |
| Methodology | Regression discontinuity exploits a sharp funding threshold |
| Discussion | Effect persists after controlling for selection and attrition |

**Ghost deck test:** Read only the action titles in sequence. They must tell the complete argument.

**Title length:** One to two lines. If more, the point isn't sharp enough yet.

**In Marp:**
```markdown
# Treatment effect is significant across all three cohorts
```
or with explicit class:
```markdown
<!-- _class: slide-results -->

# Treatment effect is significant across all three cohorts
```

---

## 3. Exhibit Discipline

### One exhibit per slide
One chart, table, diagram, or equation block per slide.

### Annotate the key finding
Mark the key data point with a callout:
```html
<div class="finding-callout">↑ 23% above baseline</div>
```

### Figure placement
Figures on the **left**, interpretive bullets on the **right**:
```html
<div class="columns-6-4">
<div>

![#center](./result.png)
###### Figure 1: Main result (Source: Jones et al., 2021)

</div>
<div>

### What to take away
- Key finding 1
- Key finding 2

</div>
</div>
```

### Prefer graphs over tables
Tables require more cognitive load. Use graphs for trends/comparisons.

### Rebuild figures from your paper
Don't screenshot from PDF. Rebuild at presentation resolution (≥ 16 pt axis labels).

### Self-sufficient slide test
Could someone understand the key point without hearing the narration? If no, add an annotation.

---

## 4. Text Discipline

### Maximum ~40 words per slide
If more, split the slide or move to appendix.

### Bullets are orientation cues
3-5 bullets per slide. Each bullet = one idea.

### Telegraphic language is acceptable
- Instead of: "Our study found that the intervention reduced costs significantly."
- Use: "Intervention reduced costs by 23% ($p < 0.01$)"

### Body font: 20 pt minimum
This is a floor. If text must be smaller than 20 pt, remove content.

### Bold and italics
- **Bold** for key terms, inline labels ("**Note:**", "**Limitation:**"), focal findings
- _Italics_ for statistical notation, species names, book titles

---

## 5. Citations and Attribution

### Cite on the slide
Every borrowed figure, claim, or dataset must have an in-slide citation.

```html
<div class="cite">
Heckman et al. (2013), Science; Cunha & Heckman (2007), AER
</div>
```

### Oral attribution
Introduce sources verbally: "Smith and colleagues found in 2022 that…"

### Figures from published sources
- Attribution caption: `###### Source: Jones et al., 2021, Fig. 3`
- Full reference on References slide

### References slide
Last slide before appendix. Complete citations.

```markdown
<!-- _class: references -->

# References

1. Author, A. & Author, B. (2024). Title. *Journal*, 10(2), 1-20.
2. ...
```

---

## 6. Deck Architecture

Required slides in order:

### Title slide
```markdown
<!-- _class: title -->

# Full Presentation Title as Statement or Question

> Venue context / subtitle

Author Name¹, Co-author Name²
¹ Institution A  ² Institution B
```

### Motivation / Context (1–2 slides)
Why this matters. Connect to a real gap or puzzle.

### Research Question (1 slide)
State it explicitly on its own slide.
```html
<div class="callout">
Do effects of the X program persist to age 35, and through which channels?
</div>
```

### Methods (1–2 slides)
Only what the audience needs to evaluate findings. Detail → appendix.

### Results (one finding per slide)
Action title states the finding. Key result annotated on the chart.

### Discussion / Implications (1–2 slides)
Interpret findings. Address main limitation(s) directly.

### Conclusions (1 slide)
- 2–4 numbered takeaways
- **Stays on screen during Q&A**
- Do NOT follow with "Thank You" or blank slide

### References
Complete citations.

### Appendix (clearly labeled)
Pre-built Q&A slides. Label: `<!-- _class: appendix -->`

---

## 7. Timing

### Slide budget
Maximum one slide per minute:
- 10-min talk: 8–10 content slides
- 15-min talk: 12–14 content slides
- 20-min talk: 15–18 content slides
- 45-min seminar: 30–40 slides

### Practice rule
Rehearse out loud. Target **1–2 minutes under** allotted time.

### Know what to cut
Mark slides to skip if time is short. Prioritize: research question → key result → conclusions.

### Q&A preparation
Pre-build appendix slides for the 3–5 most likely questions.

### End on the conclusions slide
When you say "I'll stop there," the conclusions slide must already be on screen.

---

## 8. Common Mistakes

| Mistake | Fix |
|---------|-----|
| Topic labels as titles | Write action titles (complete sentence) |
| Presenting the whole paper | Choose one argument; rest → appendix |
| Reading slides aloud | Slides carry evidence; presenter carries argument |
| Evidence without "so what" | Annotate the key finding on the chart |
| Uncited borrowed figures | Cite on slide + References slide |
| Body text < 20 pt | Remove content until it fits at 20 pt |
| Inconsistent formatting | One font, one citation style, consistent grid |
| Going over time | Rehearse under time; know what to cut |
| Ending on "Thank You" | End on conclusions slide |
| Burying the research question | Give it its own slide (slide 2–3) |
| No references slide | Always include one |

---

## 9. Marp-Specific Tips

### VS Code Setup
1. Install "Marp for VS Code" extension
2. Add theme paths to `settings.json`:
```json
"markdown.marp.themes": [
  "./css/neobeam-lgy.css",
  "./css/academic-minimal.css",
  "./css/academic-fusion.css",
  "./css/academic-full.css"
]
```

### Preview
Click the preview button (top-right) or `Ctrl+Shift+V` for side-by-side preview.

### Export
`Ctrl+Shift+P` → `Marp: Export Slide Deck` → choose PDF/PPTX/HTML.

### CLI Export
```bash
marp slides.md --theme css/neobeam-lgy.css --pdf
marp slides.md --theme css/academic-minimal.css --pptx
```

### Image paths
Use relative paths from the `.md` file:
```markdown
![#center](./figures/result.png)
```

### Math

Enable KaTeX in front matter:
```yaml
math: katex
```

**All mathematical notation MUST use LaTeX.** No plain-text math in academic slides.

**Inline** — use `$...$` for symbols and short expressions within body text:
```markdown
- 治疗组收入高 $18\%$（$p < 0.001$，$N = 2{,}400$）
- Treatment effect $\beta = 0.23$ ($SE = 0.05$, $95\%\ \text{CI}: [0.14, 0.32]$)
- 断点回归利用 $185\%$ 贫困线作为外生分配阈值
```

**Display** — use `$$...$$` for standalone equations:
```markdown
$$
Y_{it} = \alpha + \beta \cdot \text{Treat}_i + \gamma \cdot \text{Post}_t + \delta \cdot (\text{Treat}_i \times \text{Post}_t) + \varepsilon_{it}
$$
```

**Formula box** (neobeam-lgy, academic-fusion, academic-full) for key equations:
```html
<div class="formula-box">

$$
\text{ITT} = \frac{\lim_{x \downarrow c} E[Y_i | X_i = x] - \lim_{x \uparrow c} E[Y_i | X_i = x]}{\lim_{x \downarrow c} E[D_i | X_i = x] - \lim_{x \uparrow c} E[D_i | X_i = x]}
$$

</div>
```

**What requires LaTeX:**
| Category | Examples |
|----------|----------|
| p-values, t-stats, F-stats | `$p < 0.001$`, `$t = 3.42$`, `$F(2, 98) = 5.67$` |
| Greek letters | `$\alpha$`, `$\beta$`, `$\gamma$`, `$\delta$`, `$\varepsilon$` |
| Statistical notation | `$N$`, `$n$`, `$SD$`, `$SE$`, `$\mu$`, `$\sigma$` |
| Confidence intervals | `$95\%\ \text{CI}: [0.14, 0.22]$` |
| R-squared, correlations | `$R^2 = 0.34$`, `$r = 0.67$` |
| Mathematical operators | `$\times$`, `$\approx$`, `$\pm$`, `$\propto$` |
| Subscripts / superscripts | `$X_{it}$`, `$Y_{i,t-1}$`, `$10^{3}$` |
| Equations | `$y = \beta_0 + \beta_1 x + \varepsilon$` |

```markdown
❌ 治疗组显著优于对照组（p < 0.01）
❌ Treatment effect: β = 0.23 (SE = 0.05)
❌ R² = 0.34, N = 1,150

✅ 治疗组显著优于对照组（$p < 0.01$）
✅ Treatment effect: $\beta = 0.23$ ($SE = 0.05$)
✅ $R^2 = 0.34$, $N = 1{,}150$
```

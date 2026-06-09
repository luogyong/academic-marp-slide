# Marp Slide Patterns for Academic Presentations

Marp markdown patterns for each slide type. Adapted from Gabberflast/academic-pptx-skill `slide_patterns.md`.

**Theme compatibility**: 🅝 neobeam-lgy | 🅜 academic-minimal | 🅕 academic-fusion | 🅕🅤 academic-full

---

## Global Front Matter

```yaml
---
marp: true
theme: neobeam-lgy     # or academic-minimal, academic-fusion, academic-full
paginate: true
math: katex
size: 16:9
footer: '<span>Author / Institution</span><span>Title</span><span>Date</span>'
---
```

All themes: 16:9 (1280×720) default. Switch to 4:3 (960×720) via `size: 4:3`.

---

## 1. Title Slide

🅝 🅜 🅕 🅕🅤

```markdown
<!-- _class: title -->

# Treatment effect of early childhood interventions persists into adulthood across all income quartiles

> Annual Conference of the Society for Labor Economics · May 2025

Author Name¹ · Co-author Name²
¹ University X  ² Laboratory for Y
```

**Do not include:** Decorative images, clip art, animated logos (unless explicitly requested).

**Logo options** (neobeam-lgy):
```markdown
![logo-inline](./logo.png)      # Centered, visible branding
![logo](./logo.png)             # Lower-right, semi-transparent
![logo-left](./logo.png)        # Lower-left variant
```

---

## 2. Motivation / Context Slide

🅝 🅜 🅕 🅕🅤

```markdown
# Existing interventions show strong short-run effects but evidence on persistence is sparse

- **Short-run gains well established:** meta-analyses confirm positive effects at ages 5–8 (Heckman et al. 2013).
- **Long-run evidence is scarce:** only 3 RCTs track outcomes past age 25; none cover lower-income countries.
- **Mechanism is unresolved:** cognitive vs. non-cognitive channels remain debated.

<div class="cite">
Heckman et al. (2013), Science; Cunha & Heckman (2007), AER
</div>
```

**Two-column variant** (for context + gap):
```html
<div class="columns-6-4">
<div>

### What We Know
- Established finding 1
- Established finding 2

</div>
<div>

### What's Missing
- Gap in the literature
- Unresolved question

</div>
</div>
```

---

## 3. Research Question Slide

🅝 🅜 🅕 🅕🅤

```markdown
# This paper asks: do early childhood effects persist to age 35, and through which channels?

<div class="callout">
Do effects of the X program on cognitive and socio-emotional skills
at age 8 persist to age 35 outcomes (earnings, health, crime),
and does the pathway run through skills or through schooling attainment?
</div>

**Contribution:** First study to follow a randomized cohort from ages 3–5 to 35 with linked administrative records.
```

The research question gets its **own slide**. Never embed it in a motivation slide.

---

## 4. Methods Slide

🅝 🅜 🅕 🅕🅤

```markdown
# Regression discontinuity exploits a sharp household income threshold for program eligibility

<div class="columns-6-4">
<div>

### Design
- **Cohort:** 2,400 children born 1985–90 in three counties
- **Assignment:** income < $185\%$ FPL at age 3 → eligible ($N = 1{,}150$)
- **Follow-up:** ages 5, 8, 18, 25, 35 — admin records linked

</div>
<div>

### Key Outcomes
- **Primary:** age-35 earnings (log), employment
- **Secondary:** health index, criminal record indicator
- **Mechanism:** cognitive score age 8, years of schooling

</div>
</div>

<div class="cite">
Full identification assumptions and robustness checks → Appendix B
</div>
```

Target: 1–2 slides. Move procedural detail to appendix.

---

## 5. Results Slide

🅝 🅜 🅕 🅕🅤

**Critical rule:** Action title MUST state the finding, not the topic. Figure-left, interpretation-right.

```markdown
# Treated children earn 18% more at age 35 — effect is largest in the bottom income quartile

<div class="columns-6-4">
<div>

![#center](./earnings_chart.png)
###### Figure 2: Log earnings by treatment status and income quartile. Source: SSA records (2024).

<div class="finding-callout">↑ 28% for Q1</div>

</div>
<div>

### What to take away
- **Average effect:** $18\%$ earnings gain ($p < 0.001$)
- **Heterogeneity:** effects are $3.5\times$ larger for Q1 vs Q4
- **Precision:** $95\%\ \text{CI} = [14\%, 22\%]$ for pooled estimate

</div>
</div>

<div class="cite">
Administrative earnings records, Social Security Administration (accessed 2024)
</div>
```

**Checks for results slides:**
- Action title states the finding ✓
- Key result annotated on chart ✓
- Source cited at bottom ✓
- Only one chart/finding per slide ✓

---

## 6. Discussion / Implications Slide

🅝 🅜 🅕 🅕🅤

```markdown
# Results support a skill-formation pathway: the earnings effect is fully mediated by cognitive scores at age 8

### Interpretation
- Consistent with Cunha-Heckman (2007) skill complementarity: early investment compounds through schooling years.
- Schooling channel: coefficient falls to zero when conditioning on age-8 cognitive score (mediation analysis → Appendix C).

### Main limitation
- **External validity:** program implemented in three U.S. counties; generalizability requires caution.
- **Partial identification:** earnings records unavailable for 11% of cohort (attrition analysis → Appendix D).
```

Or with explicit limitation block:
```html
<div class="limitation">
External validity: program implemented in three U.S. counties; generalizability to other settings requires caution.
</div>
```

---

## 7. Conclusions Slide

🅝 (thanks) 🅜 🅕 🅕🅤

**This slide stays on screen for the entire Q&A.** Never follow with "Thank You."

```markdown
<!-- _class: conclusions -->

# Conclusions

1. **Early childhood effects are persistent:** significant earnings premium detectable at age 35, 30 years after treatment.
2. **Effects are largest for the most disadvantaged:** Q1 earnings premium (28%) is 3.5× the Q4 effect (8%).
3. **The pathway is cognitive, not schooling-mediated:** consistent with skill complementarity models.

<div class="contact">
jane.smith@university.edu  |  Working paper: bit.ly/smith2025
</div>
```

**neobeam-lgy variant** (use `<!-- _class: thanks -->`):
```markdown
<!-- _class: thanks -->

# Thanks

## Q & A

your.email@example.com
```

---

## 8. Section Divider

🅝 🅜 🅕 🅕🅤

For decks > 15 slides. Orient the audience.

```markdown
<!-- _class: section -->

# Empirical Strategy

## Identification, estimation, and robustness
```

**neobeam-lgy color variants:**
```markdown
<!-- _class: section theme-cyan -->       # Methods
<!-- _class: section theme-emerald -->    # Results
<!-- _class: section theme-indigo -->     # AI / Algorithm
<!-- _class: section theme-violet -->     # Discussion
<!-- _class: section theme-burgundy -->   # Challenges
<!-- _class: section theme-graphite -->   # Architecture
<!-- _class: section theme-amber -->      # Findings
```

**academic-full variant:**
```markdown
<!-- _class: slide-section -->

<div class="section-num">Part 2</div>

# Empirical Strategy

## Identification, estimation, and robustness
```

---

## 9. Breadcrumb Bar

🅕🅤 (academic-full only)

Persistent navigation for talks > 15 minutes. Add to every content slide:

```html
<div class="breadcrumb-bar">
  <span>Motivation</span>
  <span>Data</span>
  <span class="active">Strategy</span>
  <span>Results</span>
  <span>Discussion</span>
</div>
```

Shift all slide content down automatically (CSS `section:has(.breadcrumb-bar)` handles padding).

---

## 10. References Slide

🅝 🅜 🅕 🅕🅤

```markdown
<!-- _class: references -->

# References

1. Cunha, F. & Heckman, J.J. (2007). The Technology of Skill Formation. *American Economic Review*, 97(2), 31–47.
2. Heckman, J.J. et al. (2013). The Rate of Return to the HighScope Perry Preschool Program. *Journal of Public Economics*, 94(1), 114–128.
3. Smith, J. & Doe, J. (2025). Long-Run Returns to Early Childhood Intervention. *Working paper*.
```

---

## 11. Appendix Slide

🅝 🅜 🅕 🅕🅤

Pre-built Q&A slides. Label clearly:

```markdown
<!-- _class: appendix -->

# Earnings effect is stable across bandwidth choices and polynomial specifications

## Appendix B — Robustness Checks

<div class="columns-6-4">
<div>

![#center](./robustness.png)

</div>
<div>

- Bandwidth: ±10% to ±25% FPL
- Polynomial: linear to cubic
- Result: effect stable across all specs

</div>
</div>
```

---

## Quick Reference: Component Cheat Sheet

### Boxes & Alerts

| Component | Marp HTML | Themes |
|-----------|-----------|--------|
| Info box | `<div class="box info" data-label="Note">...</div>` | 🅝 🅕 🅕🅤 |
| Success box | `<div class="box success" data-label="Finding">...</div>` | 🅝 🅕 🅕🅤 |
| Warning box | `<div class="box warn" data-label="Caution">...</div>` | 🅝 🅕 🅕🅤 |
| Alert box | `<div class="box alert" data-label="Important">...</div>` | 🅝 |
| Theorem box | `<div class="box theorem" data-label="Theorem 1">...</div>` | 🅝 |
| Proof | `<div class="proof" data-label="Proof">...</div>` | 🅝 🅕 🅕🅤 |
| Formula box | `<div class="formula-box">$$...$$</div>` | 🅝 🅕 🅕🅤 |
| Citation | `<div class="cite">Author (Year), Journal</div>` | 🅝 🅕 🅕🅤 |
| Callout | `<div class="callout">Research question?</div>` | 🅜 🅕 🅕🅤 |
| Limitation | `<div class="limitation">Caveat here</div>` | 🅜 🅕🅤 |

### Beamer Blocks (🅝 🅕 🅕🅤)

```html
<div class="beamer theme" data-label="Takeaway">...</div>
<div class="beamer example" data-label="Example">...</div>
<div class="beamer warn" data-label="Warning">...</div>
```

### Columns

| Ratio | Class |
|-------|-------|
| 1:1 | `columns` or `columns-5-5` |
| 7:3 | `columns-7-3` |
| 6:4 | `columns-6-4` |
| 4:6 | `columns-4-6` |
| 3:7 | `columns-3-7` |
| 1:1:1 | `columns-3` |
| 1:1:1:1 | `columns-4` |

### Layout Helpers (all themes)

| Class | Effect |
|-------|--------|
| `.center` | Center text |
| `.left` / `.right` | Align text |
| `.mt-1` `.mt-2` `.mt-3` | Margin top |
| `.mb-1` `.mb-2` `.mb-3` | Margin bottom |
| `.lh-1` `.lh-2` `.lh-3` | Line height |
| `.fill` | Flex fill remaining space |
| `.row` | Horizontal flex row |

---

## Quick Checks Before Delivery

```
□ Title slide: full title as statement/question, author, affiliation, venue, date
□ Every content slide: action title (complete sentence, states takeaway)
□ Ghost deck test: titles alone tell the complete argument
□ Results slides: one exhibit each, key finding annotated on chart
□ Every borrowed figure/data point: in-slide citation
□ References slide: complete, consistently formatted
□ Conclusions slide: last main slide, stays on screen during Q&A
□ Contact info on conclusions or final slide
□ Body text ≥ 20 pt (in minimal themes)
□ No slide has > ~40 words of body text
□ Appendix slides labeled, with pre-built Q&A answers
□ Theme CSS path configured in VS Code settings
□ Deck runs 1–2 minutes under the time limit when practiced aloud
```

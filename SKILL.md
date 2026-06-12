---
name: academic-marp-slide
description: "Create academic presentations as Marp markdown with neobeam-lgy theme ecosystem. Use when the user wants conference talks, seminar slides, thesis defenses, grant briefings, lab meetings, or any academic presentation as Marp markdown. Triggers (EN): 'conference talk', 'seminar slides', 'thesis defense', 'research presentation', 'academic deck', 'make slides for my paper', 'Marp presentation', 'academic marp'. Triggers (ZH): '学术PPT', '组会PPT', '论文PPT', '答辩PPT', '学术汇报', '课程PPT', '学术演示', '做幻灯片', '生成PPT', 'Marp幻灯片'. This skill governs CONTENT and STRUCTURE. For the CSS themes, see css/ directory."
license: MIT
---

# Academic Marp Slide Skill / 学术 Marp 幻灯片技能

Generate academic presentations as **Marp markdown** — enforced action titles, structured argument, communication-first design. Powered by the neobeam-lgy theme ecosystem.

## Language Support / 语言支持

**Auto-detect and match the user's language.** This skill supports bilingual (EN/ZH) operation:

| 用户语言 | 你的工作语言 | 幻灯片内容语言 | 默认主题 |
|----------|-------------|---------------|---------|
| 中文 | 中文 | 中文 | `neobeam-lgy` |
| English | English | English | `academic-minimal` |
| 中英混合 | 中文 | 中文为主 | `neobeam-lgy` |

**核心原则:**
- 用户说中文 → 用中文思考和回复，生成中文幻灯片内容
- 用户说英文 → 用英文思考和回复，生成英文幻灯片内容
- 学术概念术语（Action Title、Ghost Deck Test 等）用英文原名，解释用用户语言
- 中文幻灯片默认使用 `neobeam-lgy` 主题（最佳 CJK 字体 + 丰富组件）
- 中文 trigger 关键词：学术PPT、组会PPT、论文PPT、答辩PPT、学术汇报、课程PPT、做幻灯片

## How This Skill Works / 工作机制

1. **SKILL.md** (this file) — content strategy, argument structure, design standards, theme selection
2. **[content_guidelines.md](content_guidelines.md)** — detailed academic writing rules adapted for Marp
3. **[slide_patterns_marp.md](slide_patterns_marp.md)** — per-slide-type Marp patterns

Output is **Marp markdown** (`.md`), rendered with one of four CSS themes in `css/`.

---

## PDF Input: MinerU Extraction (Pre-Processing Step)

**If the input is a PDF file, ALWAYS extract it with MinerU before generating slides.**

MinerU converts the PDF to Markdown with all figures preserved as image references — this is the only way to reliably use the paper's own figures in slides.

### Extraction Command

Use the MinerU Open API MCP tool (tool name: `mineru-open-api`):

```
Input:  path/to/paper.pdf
Output: path/to/paper.md   ← same directory as the PDF, same filename
```

The extracted `.md` file will contain:
- Full text in Markdown
- Image references like `![](images/figure_1.png)` pointing to a sibling `images/` folder

### After Extraction

1. Read the extracted `.md` to get the full text (use this instead of the PDF for content)
2. Inventory all figures: collect every `![](...)` path in the extracted md
3. Map each figure to the section it appears in (methods figure, results figure, etc.)
4. Use these figures when building slides (see Image Integration below)

**Do not skip extraction even if you already have the PDF text** — the image paths only come from MinerU's output.

---

## Theme Selection

Four themes available — choose based on the presentation context:

| Theme | CSS File | Style | Best For |
|-------|----------|-------|----------|
| **neobeam-lgy** | `neobeam-lgy.css` | Rich academic (gradients, multi-color boxes, beamer blocks) | Chinese academic, course lectures, comprehensive talks |
| **academic-minimal** | `academic-minimal.css` | Minimalist (white bg, navy+blue, single font, no decoration) | High-impact conference talks, strict slide_patterns.md |
| **academic-fusion** | `academic-fusion.css` | Blend (neobeam components + minimal palette) | Balanced academic presentations |
| **academic-full** | `academic-full.css` | Full slide patterns (all 10 patterns as CSS classes) | Complex decks needing explicit pattern control |

### Default Theme Logic / 默认主题规则

- **中文内容（教学/汇报/答辩）**: 默认 `neobeam-lgy`（CJK 字体栈最完整、box/beamer 组件最丰富）
- **English conference talk**: 默认 `academic-minimal`（slide_patterns.md 极简哲学）
- **用户不确定**: 用中文询问偏好，展示上方表格

### 中文用户的幻灯片写作规范

生成中文幻灯片时，遵循以下额外规范：

**Action Title（行动标题）** — 每页标题必须是完整断言句：
| 不要写（主题标签） | 要写（行动标题） |
|-------------------|-----------------|
| 实验结果 | 治疗组在三个队列中均显著优于对照组（$p<0.01$）|
| 文献综述 | 现有研究未解释因果机制，留下关键空白 |
| 方法 | 断点回归利用 $185\%$ 贫困线作为外生分配阈值 |

**中英混排** — 学术术语保留英文，正文用中文：
```markdown
# BERT 预训练目标与 MLM 遮蔽策略显著影响下游 NER 性能
```

**引用格式** — 中文幻灯片使用 `（作者, 年份）` 格式：
```html
<div class="cite">
（Heckman et al., 2013, Science）
</div>
```

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

**Image assignment**: during outlining, note which figure from the paper best illustrates each key slide. Assign figures greedily — the most important figure goes in the main body; all others go to the appendix.

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
Significant effect at $p < 0.001$
</div>
```

**Beamer blocks**:
```html
<div class="beamer theme" data-label="Takeaway">
Main conclusion here
</div>
```

**Formula box** (neobeam-lgy, academic-fusion, academic-full):
```html
<div class="formula-box">

$$
Y_{it} = \alpha + \beta \cdot \text{Treat}_i + \gamma \cdot \text{Post}_t + \delta \cdot (\text{Treat}_i \times \text{Post}_t) + \varepsilon_{it}
$$

</div>
```

**Inline math** — every statistical symbol gets `$...$`:
```markdown
- 核心发现：处理组收入高 $18\%$（$p < 0.001$，$N = 2{,}400$）
- 效应量 $\beta = 0.23$，$95\%\ \text{CI}: [0.14, 0.32]$
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

### Image Integration / 图片集成规范

**Images are mandatory when the source paper has figures.** Text-only slides for results, methods, or framework are a quality failure.

#### Placement rules

| Slide type | Image usage |
|------------|-------------|
| Results / findings | One figure per slide, left or center; bullet "so what" on the right |
| Methods / framework | Architecture diagram or pipeline figure if available |
| Introduction / motivation | Conceptual diagram or data overview figure |
| Conclusions | Optional — repeat the single most impactful figure |
| Background / related work | Only if the figure directly supports the argument |

#### Marp image syntax

**Full-width centered image:**
```markdown
![w:700px center](images/figure_3.png)
*图3：主要实验结果——处理组在所有三个队列中均显著优于对照组*
```

**Two-column: figure left + takeaway right:**
```html
<div class="columns-6-4">
<div>

![w:100%](images/figure_2.png)
*图2：回归不连续设计示意图*

</div>
<div>

### 关键发现
- 贫困线两侧存在显著跳跃（$\beta = 0.23$）
- 带宽敏感性检验通过

</div>
</div>
```

**Figure with caption box** (neobeam-lgy):
```html
<div class="box info" data-label="图1：研究框架">

![w:650px center](images/figure_1.png)

</div>
```

#### Image path convention

Always use paths relative to the output `.md` file:
- MinerU output: `images/figure_1.png` (MinerU creates an `images/` subfolder)
- User-provided images: use the path as given

If an image path is uncertain, write `<!-- TODO: 替换为实际图片路径 -->` below the `![]()` line as a placeholder comment.

---

### Image Appendix / 图片附录

**After the References slide, add an appendix section listing ALL figures from the source paper.** This lets the presenter pull any figure up during Q&A and provides a reference for later editing.

#### Appendix structure

```markdown
---
<!-- _class: section -->

# 附录：原文图表

---
<!-- _class: appendix -->

# 附录 A — 图1：[图题]

![w:750px center](images/figure_1.png)

**说明：** [一句话描述图的内容和位置，例如"来自第3节，展示研究框架总览"]

---
<!-- _class: appendix -->

# 附录 B — 图2：[图题]

![w:750px center](images/figure_2.png)

**说明：** [描述]

---
```

Rules:
- Every figure from the MinerU-extracted md gets one appendix slide
- Slide title = `附录 X — 图N：[caption from paper]`
- Caption = one sentence: what the figure shows + where it appears in the paper
- Figures already used in the main body are still included in the appendix (for reference)
- Order: same order as they appear in the paper

#### QA for appendix

After writing the appendix, count: number of `![](...)` in the extracted md == number of appendix slides. If they don't match, you missed a figure.

### Math Formula Convention / 数学公式规范

**All mathematical notation MUST use LaTeX.** This is non-negotiable — plain-text math is not acceptable in academic slides.

**Inline formulas** — use `$...$` for symbols and short expressions within text:
```markdown
- 治疗组显著优于对照组（$p < 0.01$）
- 干预组收入高出 $18\%$（$95\%\ \text{CI}: [14\%, 22\%]$）
- 处理效应 $\beta = 0.23$，标准误 $SE = 0.05$
- 样本量 $N = 1{,}150$，覆盖 $40$ 年面板数据
```

**Display formulas** — use `$$...$$` for standalone equations and key formulas:
```markdown
$$
Y_{it} = \alpha + \beta \cdot \text{Treat}_i + \gamma \cdot \text{Post}_t + \delta \cdot (\text{Treat}_i \times \text{Post}_t) + \varepsilon_{it}
$$
```

**Formula box** — for key equations that need emphasis (neobeam-lgy, academic-fusion, academic-full):
```html
<div class="formula-box">

$$
\text{ITT} = \frac{\lim_{x \downarrow c} E[Y_i | X_i = x] - \lim_{x \uparrow c} E[Y_i | X_i = x]}{\lim_{x \downarrow c} E[D_i | X_i = x] - \lim_{x \uparrow c} E[D_i | X_i = x]}
$$

</div>
```

**What MUST use LaTeX:**
| 类型 | 示例 |
|------|------|
| p-values, t-stats, F-stats | `$p < 0.001$`, `$t = 3.42$`, `$F(2, 98) = 5.67$` |
| Greek letters | `$\alpha$`, `$\beta$`, `$\gamma$`, `$\delta$`, `$\varepsilon$` |
| Statistical notation | `$N$`, `$n$`, `$SD$`, `$SE$`, `$\mu$`, `$\sigma$` |
| Confidence intervals | `$95\%\ \text{CI}: [0.14, 0.22]$` |
| R-squared, correlations | `$R^2 = 0.34$`, `$r = 0.67$` |
| Mathematical operators | `$\times$`, `$\approx$`, `$\pm$`, `$\propto$` |
| Subscripts / superscripts | `$X_{it}$`, `$Y_{i,t-1}$`, `$10^{3}$` |
| Equations (any) | `$y = \beta_0 + \beta_1 x + \varepsilon$` |
| Percentages in stats context | `$18\%$` vs. `$23\%$` |

**Counterexamples** — plain text is WRONG:
```markdown
❌ 治疗组显著优于对照组（p < 0.01）
❌ Treatment effect: β = 0.23 (SE = 0.05)
❌ R² = 0.34, N = 1,150
❌ Y = α + β·Treat + ε
```

**Correct versions:**
```markdown
✅ 治疗组显著优于对照组（$p < 0.01$）
✅ Treatment effect: $\beta = 0.23$ ($SE = 0.05$)
✅ $R^2 = 0.34$, $N = 1{,}150$
✅ $Y = \alpha + \beta \cdot \text{Treat} + \varepsilon$
```

> **Note:** `math: katex` is required in the Marp front matter for LaTeX rendering. This is already in the front matter template.

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
□ All math symbols and formulas use LaTeX $...$ or $$...$$ (no plain-text math)
□ [PDF input] MinerU extraction completed; extracted .md saved next to source PDF
□ [PDF input] Key slides include figures from the paper (results/methods/framework)
□ [PDF input] Image appendix present: one slide per figure, with description
□ [PDF input] Appendix figure count == figure count in extracted .md
```

---

## Key Principles

1. **Action titles, not topic labels.** Every slide title is a complete sentence. Reading titles alone tells the whole argument.
2. **One argument, made well.** Pick the claim that fits the time. Everything else → appendix.
3. **One insight per slide.** One exhibit per results slide. Annotate the key finding.
4. **Slides support speech; they don't replace it.** Body text orients; the presenter argues.
5. **Cite everything borrowed.** In-slide citation + References slide.
6. **End on conclusions.** Conclusions slide stays on screen during Q&A.
7. **All math in LaTeX.** Every symbol, formula, equation — inline `$...$`, display `$$...$$`. No plain-text math.
8. **Figures are mandatory for PDF inputs.** Extract with MinerU first, embed key figures in the body, put all figures in the appendix. Text-only results slides are a quality failure.

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

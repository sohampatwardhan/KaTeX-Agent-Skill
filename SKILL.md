---
name: katex
description: Use when writing, formatting, or debugging math expressions, equations, or LaTeX in Markdown that must render with KaTeX — GitHub Markdown/READMEs, Joplin notes, GitLab, Jupyter, Notion, or any KaTeX viewer. Covers inline vs block delimiters, the GitHub/Joplin dollar-sign rules, multi-line/aligned equations, matrices, cases, and which LaTeX commands KaTeX does NOT support.
---

# Writing Math for KaTeX (GitHub, Joplin, and other KaTeX viewers)

## Overview

KaTeX renders a **large subset of LaTeX math**, not all of it. Math that compiles in a full LaTeX document can silently fail or show a red error in KaTeX. The two most common ways math breaks are (1) using the wrong **delimiters** for the host (GitHub/Joplin only enable `$` and `$$`), and (2) using a LaTeX command KaTeX doesn't support.

**Core rule:** delimiters are chosen by the *host* (GitHub, Joplin, …); the math *inside* them is the KaTeX subset. Get both right and it renders identically everywhere.

## Delimiters (choose by host)

| Host | Inline | Block / display |
|------|--------|-----------------|
| **GitHub Markdown** | `$ ... $` | `$$ ... $$` on their own lines, **or** a ```` ```math ```` fenced block |
| **Joplin** | `$ ... $` | `$$ ... $$` |
| **GitLab / Jupyter / Notion / VS Code preview** | `$ ... $` | `$$ ... $$` |

**Never use `\( ... \)` or `\[ ... \]`** — these LaTeX delimiters are *not* enabled in GitHub or Joplin Markdown and will show up as literal text.

## The dollar-sign rules (the #1 source of broken output)

These apply to GitHub and Joplin (both parse `$` as a math delimiter):

1. **No space just inside inline delimiters.** Write `$x^2$`, not `$ x^2 $`. A leading/trailing space can stop it from parsing as math.
2. **Escape a literal dollar sign as `\$`.** Writing "it costs $5 and $6" makes the parser treat the text between the two `$` as math. Use `it costs \$5 and \$6`. This renders as a plain `$` in both GitHub and Joplin.
3. **Put block `$$ ... $$` on their own lines**, separated from surrounding text by a blank line above and below. GitHub in particular needs this.
4. **Keep `&` `<` `>` literal inside math.** Do not HTML-escape them to `&amp;` / `&lt;` — KaTeX needs a raw `&` as the alignment separator in `aligned`/`matrix`/`cases`, and `&amp;` will break the layout. (This bites when math is pasted through an HTML-escaping tool.)

## Quick reference (copy-paste patterns)

All of the following go *inside* `$...$` (inline) or `$$...$$` (block):

| Want | Write |
|------|-------|
| Fraction | `\frac{a}{b}` |
| Superscript / subscript | `x^2`, `x_i`, `x_{i+1}`, `x^{2n}` |
| Square / n-th root | `\sqrt{x}`, `\sqrt[3]{x}` |
| Greek | `\alpha \beta \gamma \pi \Sigma \Omega` |
| Sum / integral / product with limits | `\sum_{i=1}^{n}`, `\int_0^1`, `\prod_{k=1}^{n}` |
| Limit | `\lim_{h \to 0}` |
| Named operators | `\sin \cos \log \ln \exp \max \min \gcd` |
| Custom operator | `\operatorname{sinc}` |
| Binomial | `\binom{n}{k}` |
| Text inside math | `\text{if } x \ge 0` |
| Vectors / bold | `\vec{v}`, `\mathbf{A}`, `\hat{x}`, `\bar{x}`, `\overline{AB}` |
| Number sets | `\mathbb{R} \; \mathbb{Z} \; \mathbb{N} \; \mathbb{Q} \; \mathbb{C}` |
| Relations / membership | `\in \notin \subseteq \subset \cup \cap \le \ge \ne \approx \equiv` |
| Arrows | `\to \rightarrow \Rightarrow \iff \mapsto` |
| Dots | `\cdots \ldots \vdots \ddots` |
| Auto-sized delimiters | `\left( \frac{a}{b} \right)`, `\left[ \right]`, `\left\{ \right\}`, `\left\lvert \right\rvert` |
| Spacing | `\,` (thin) `\;` (thick) `\quad` `\qquad` `\!` (negative) |
| Equation number | `\tag{1}` |

## Multi-line and structured math

Multiple lines require an **environment**, not bare newlines. In GitHub/Joplin you place the environment *inside* `$$ ... $$` (you cannot use `\begin{align}` as a standalone delimiter). Use `&` to align columns and `\\` to end a row.

```markdown
$$
\begin{aligned}
(a+b)^2 &= (a+b)(a+b) \\
        &= a^2 + 2ab + b^2
\end{aligned}
$$
```

| Need | Environment (inside `$$`) |
|------|---------------------------|
| Aligned steps (align on `&`) | `aligned` |
| Centered lines, no alignment | `gathered` |
| Piecewise / cases | `cases` |
| Matrix (parens/brackets/bars) | `pmatrix` / `bmatrix` / `vmatrix` / `matrix` |
| Custom column matrix | `array` |

Examples:

```markdown
$$
f(x) = \begin{cases} x^2 & \text{if } x \ge 0 \\ -x & \text{if } x < 0 \end{cases}
$$

$$
\begin{pmatrix} a & b \\ c & d \end{pmatrix}
\begin{pmatrix} x \\ y \end{pmatrix}
= \begin{pmatrix} ax + by \\ cx + dy \end{pmatrix}
$$
```

## Commands KaTeX does NOT support (avoid these)

Using these produces a KaTeX error, not a fallback. Substitute the right column.

| Unsupported | Use instead |
|-------------|-------------|
| `\label` / `\ref` / `\eqref` | No cross-referencing; number manually with `\tag{1}` |
| `eqnarray` environment | `aligned` (inside `$$`) |
| standalone `\begin{align}` as a delimiter | wrap the environment in `$$ ... $$` |
| `\require{...}` (e.g. loading mhchem) | not available on GitHub; on Joplin mhchem `\ce{}` works only if the plugin is enabled |
| `\newenvironment` / `\renewenvironment` | define a macro with `\def` / `\newcommand` instead |
| `\includegraphics` | not supported — use a Markdown image outside the math |
| `\setlength` / `\scalebox` / `\shoveleft` / `\shoveright` | not supported — restructure the expression |
| `\begin{subarray}` (older KaTeX) | verify against target version; prefer `\substack{...}` |

Macros **are** supported: `\def`, `\gdef`, `\newcommand`, `\renewcommand` with up to 9 args (`#1`…`#9`).

**Full alphabetical support/unsupported table:** see `references/support-table.md` for the complete list of supported functions, symbols, and environments, and the exact commands KaTeX rejects.

## Common mistakes

| Symptom | Cause | Fix |
|---------|-------|-----|
| Math shows as literal `\(...\)` text | Wrong delimiters | Use `$...$` / `$$...$$` |
| A sentence with a price renders half as math | Unescaped literal `$` | Escape as `\$` |
| Block equation not rendering on GitHub | No blank line around `$$` | Add blank lines above and below |
| `aligned`/`cases`/matrix collapses to one column | `&` was HTML-escaped to `&amp;` | Keep `&` raw |
| Red "unsupported command" error | Command outside KaTeX subset | Check `references/support-table.md` and substitute |
| Multi-line equation shows on one line | Bare newlines instead of an environment | Wrap in `aligned`/`gathered` with `\\` |
| Delimiters too small around a tall fraction | Fixed-size `( )` | Use `\left( ... \right)` |

## Verification

If you can, confirm rendering rather than assuming: preview the note in Joplin, or push to a GitHub gist/README and view it. When you cannot preview, stick to the Quick Reference patterns above (all confirmed in the KaTeX subset) and avoid anything in the unsupported table.

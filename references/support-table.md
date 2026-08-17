# KaTeX Support Reference

Curated from the official KaTeX docs (`docs/supported.md`, `docs/support_table.md`) via Context7. KaTeX renders a large subset of LaTeX **math mode**. This file lists what you can rely on and what KaTeX rejects. For host delimiter rules (GitHub/Joplin), see `../SKILL.md`.

When in doubt, the authoritative, always-current lists are:
- Supported functions: https://katex.org/docs/supported
- Full support table: https://katex.org/docs/support_table
- Known gaps: https://github.com/KaTeX/KaTeX/wiki/Things-that-KaTeX-does-not-(yet)-support

---

## Accents

`\hat{x}` `\bar{x}` `\vec{x}` `\dot{x}` `\ddot{x}` `\tilde{x}` `\acute{x}` `\grave{x}` `\breve{x}` `\check{x}` `\overline{AB}` `\underline{AB}` `\widehat{abc}` `\widetilde{abc}` `\overrightarrow{AB}` `\overleftarrow{AB}` `\overbrace{...}` `\underbrace{...}`

## Delimiters (grow with `\left`/`\right`)

Parentheses `( )`, brackets `[ ]`, braces `\{ \}`, `\lvert \rvert` (`|`), `\lVert \rVert` (`\|`), `\langle \rangle`, `\lceil \rceil`, `\lfloor \rfloor`, `/`, `\backslash`, `\uparrow \downarrow \Uparrow \Downarrow`.

Auto-size: `\left( \frac{a}{b} \right)`. Manual sizes: `\big \Big \bigg \Bigg` (and `l`/`r` variants like `\bigl \bigr`). Use `\left. ... \right)` when one side has no delimiter.

## Fractions and binomials

`\frac{a}{b}` `\dfrac{a}{b}` (display size) `\tfrac{a}{b}` (text size) `\cfrac{a}{b}` (continued) `\binom{n}{k}` `\dbinom` `\tbinom` `\genfrac{}{}{}{}{}{}` `a \over b` `a \choose b`

## Roots

`\sqrt{x}` `\sqrt[3]{x}`

## Sub/superscripts and limits

`x^2` `x_i` `x_i^2` `x_{i+1}^{2n}` `\sum_{i=1}^{n}` `\int_0^1` `\oint` `\iint` `\iiint` `\prod` `\coprod` `\bigcup \bigcap \bigoplus \bigotimes \bigvee \bigwedge \biguplus`. Force limit position with `\limits` / `\nolimits` and `\sideset`.

## Named operators (upright, correct spacing)

`\sin \cos \tan \cot \sec \csc` `\arcsin \arccos \arctan` `\sinh \cosh \tanh \coth` `\log \ln \lg \exp` `\lim \limsup \liminf` `\max \min \sup \inf` `\det \dim \ker \deg \gcd \hom \arg \Pr` `\bmod` `a \pmod{n}` `\pod{n}`.

Custom operator: `\operatorname{sinc}` (upright) or `\operatorname*{argmax}\limits_x` (with limits).

## Greek letters

Lowercase: `\alpha \beta \gamma \delta \epsilon \varepsilon \zeta \eta \theta \vartheta \iota \kappa \lambda \mu \nu \xi \pi \varpi \rho \varrho \sigma \varsigma \tau \upsilon \phi \varphi \chi \psi \omega`

Uppercase: `\Gamma \Delta \Theta \Lambda \Xi \Pi \Sigma \Upsilon \Phi \Psi \Omega`

## Letters and number sets

`\mathbb{R}` (blackboard: R Z N Q C H) `\mathcal{L}` (calligraphic) `\mathfrak{g}` (fraktur) `\mathbf{v}` (bold) `\mathit{x}` `\mathrm{d}` (upright) `\mathsf{X}` `\mathtt{X}` `\boldsymbol{\alpha}` `\bm{v}`.

## Relations, membership, logic

`= \ne \neq \equiv \approx \cong \sim \simeq \propto \asymp` `< > \le \leq \ge \geq \ll \gg` `\in \notin \ni \subset \subseteq \subsetneq \supset \supseteq \sqsubseteq` `\cup \cap \setminus \emptyset \varnothing` `\forall \exists \nexists \neg \land \lor \implies \impliedby \iff \therefore \because \mid \nmid \parallel \perp`.

## Binary operators

`+ - \times \div \pm \mp \cdot \ast \star \circ \bullet \oplus \ominus \otimes \oslash \odot \cup \cap \uplus \sqcup \sqcap \wedge \vee \triangleleft \triangleright \wr \amalg`.

## Arrows

`\to \gets \leftarrow \rightarrow \leftrightarrow \Leftarrow \Rightarrow \Leftrightarrow \longrightarrow \longleftarrow \Longrightarrow \iff \mapsto \longmapsto \hookrightarrow \hookleftarrow \nearrow \searrow \nwarrow \swarrow \uparrow \downarrow \rightharpoonup \leftharpoondown \xrightarrow[under]{over} \xleftarrow{...}`.

## Dots and misc symbols

`\ldots \cdots \vdots \ddots \dots` `\infty \partial \nabla \prime \emptyset \angle \triangle \square \Box \diamond \aleph \hbar \ell \Re \Im \wp \S \dagger \ddagger \flat \natural \sharp \clubsuit \diamondsuit \heartsuit \spadesuit \checkmark`.

## Text and formatting inside math

`\text{plain text}` (upright, keeps spaces) `\textbf{...}` `\textit{...}` `\textrm{...}` `\texttt{...}` `\textsf{...}` `\textnormal{...}` `\emph{...}`. Sizes: `\tiny \scriptsize \small \normalsize \large \Large \LARGE \huge \Huge`. Color: `\color{red}{x}`, `\textcolor{blue}{y}`, `\colorbox{yellow}{z}`, `\fcolorbox{red}{yellow}{z}` (CSS names or `#RRGGBB`).

## Spacing

`\,` (thin, 3mu) `\:` / `\medspace` (4mu) `\;` / `\thickspace` (5mu) `\!` (negative thin) `\ ` (word space) `\quad` `\qquad` `\enspace` `\hspace{1em}` `\hspace*{1em}` `\phantom{x}` `\hphantom{x}` `\vphantom{x}` `\mkern` `\mspace`.

## Environments (wrap inside `$$ ... $$` on GitHub/Joplin)

Alignment / multi-line: `aligned` `gathered` `split` `align` `align*` `alignat` `alignat*` `gather` `gather*` `equation` `equation*` `cases` `rcases` `darray` `dcases`.

> On GitHub/Joplin you **cannot** use `\begin{align}` as a standalone block delimiter — put the environment inside `$$ ... $$` (e.g. `aligned`).

Matrices: `matrix` `pmatrix` `bmatrix` `Bmatrix` `vmatrix` `Vmatrix` `smallmatrix` `array`. Column spec for `array`: `\begin{array}{c:c|c}` (`c`/`l`/`r`, `:` dashed rule, `|` solid rule; `\hline` and `\hdashline` for horizontal rules). Adjust row height with `\def\arraystretch{1.5}`.

Equation numbering: `\tag{1}`, `\tag*{...}` (no parentheses), `\notag`. Sub-stacks: `\substack{i<n \\ j<m}`, `subarray`.

Commutative diagrams: `\begin{CD} ... \end{CD}` (with `@>>>` `@<<<` `@VVV` `@AAA` `@=` `@.`).

## Macros (supported)

`\def\name{...}`, `\newcommand{\name}[nargs]{...}`, `\renewcommand`, `\gdef`, `\global\def`, `\let`, `\edef`, `\xdef`, `\futurelet`. Up to 9 arguments (`#1`…`#9`). `\gdef`/`\xdef`/`\global\def` persist across expressions on a page. `\long` is ignored (all macros are long).

## Other useful commands

`\overset{a}{b}` `\underset{a}{b}` `\stackrel{a}{b}` `\overbrace{}^{}` `\underbrace{}_{}` `\boxed{x}` `\cancel{x}` `\bcancel{x}` `\xcancel{x}` `\sout{x}` `\href{url}{text}` `\htmlClass` (if `trust` enabled) `\rule{w}{h}` `\raisebox{d}{...}` `\smash{...}` `\char"263A` `\KaTeX` `\TeX` `\LaTeX`.

---

## NOT supported (will error — do not use)

KaTeX throws (or shows a red error) rather than falling back for these. Substitutions in parentheses.

- **Cross-referencing:** `\label` `\ref` `\eqref` `\cite` `\pageref` → number manually with `\tag{}`.
- **Loading packages:** `\require` (so mhchem `\ce{}`, physics package, etc. are unavailable on GitHub; Joplin only if its plugin is enabled).
- **Deprecated multi-line:** `eqnarray` (→ `aligned` / `align`).
- **Standalone `\begin{align}`/`\begin{equation}` as delimiters** on GitHub/Joplin (→ wrap in `$$`).
- **Environment definition:** `\newenvironment` `\renewenvironment` (→ use `\newcommand`/`\def`).
- **Graphics/layout:** `\includegraphics` `\scalebox` `\resizebox` `\rotatebox` `\setlength` `\addtolength` `\parbox` `\minipage`.
- **Alignment tweaks:** `\shoveleft` `\shoveright` `\leftroot` `\uproot` `\intertext` (limited).
- **Fonts/misc:** `\sc` `\sl` `\textsc` `\textsl` `\Tiny` (→ `\tiny`) `\Huge` variants beyond the size list above, `\style`, `\toggle`, `\texttip`, `\skew`, `\sideset` (partial), `\Space`, `\strut`, `\smiley`.
- **TeX plumbing:** `\par` (so paragraph breaks and `\long` are no-ops), `\skip`, `\lower`/`\raise` (use `\raisebox`), `\vfil` `\vfill` `\vline` `\hfil` (limited), `\abovewithdelims` `\atopwithdelims`.

If a command isn't in this file, check https://katex.org/docs/support_table before using it — the supported set grows between KaTeX releases, and the host (GitHub/Joplin) may ship an older KaTeX than the latest docs describe.

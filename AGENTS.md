# Agent Notes

This file records project-specific conventions for AI agents and collaborators. Keep user-facing documentation in `README.md`; use this file for workflow memory and maintenance rules.

## Scope

- Work primarily inside this `MZ-Latex-Template` project.
- Treat sibling folders such as `REF/` as reference material unless the user explicitly asks to modify them.
- Keep edits focused on the requested template behavior. Avoid unrelated rewrites or style churn.

## Build

- Match the user's Overleaf compiler settings for projects based on this template:
  - Main document: `main.tex`.
  - Compiler: XeLaTeX.
  - TeX Live version: 2025.
  - Compile mode: Normal.
- Compile locally with XeLaTeX from the project root and write all generated files to `output/`:

```powershell
xelatex -interaction=nonstopmode -halt-on-error -output-directory=output main.tex
xelatex -interaction=nonstopmode -halt-on-error -output-directory=output main.tex
```

- The second run refreshes the table of contents and cross references.
- Keep the local `output/` directory. It is intentionally ignored by Git through `.gitignore`.
- Do not compile into the project root. If root-level `main.aux`, `main.log`, `main.pdf`, `main.toc`, `main.xdv`, or similar build artifacts appear, remove them and rebuild into `output/`.
- Do not delete `output/` just to clean status unless the user explicitly asks.

## LaTeX Style

- Global packages and reusable environments belong in `styles/report-style.sty`.
- Chapter examples and document content belong in `chapters/*.tex`.
- The template uses `ctexrep` with XeLaTeX.
- Chinese body text is configured globally in `styles/report-style.sty` as SimSun/宋体. Keep this unless the user requests another Chinese font.
- English/Latin text is configured globally in `styles/report-style.sty` and should remain Times New Roman unless the user requests another font.
- The current report style should stay close to the user's old acceptance-report template: compact body spacing, compact heading spacing, dense test-case blocks, and formal black-rule tables.
- On Overleaf, ensure licensed system fonts used by the project are available or uploaded with the project if Overleaf cannot resolve them directly.
- Prefer packages that compile without shell escape for default template features.
- Heading levels are defined by LaTeX command level: `\chapter` is 一级标题, `\section` is 二级标题, `\subsection` is 三级标题, `\subsubsection` is 四级标题, `\paragraph` is 五级标题, and `\subparagraph` is 六级标题.

## Code Listings

- Use the `cbox` environment for C code examples:

```tex
\begin{cbox}{Example Title}
int main(void)
{
  return 0;
}
\end{cbox}
```

- `cbox` is defined with `tcolorbox + listings` in `styles/report-style.sty`.
- The current C highlighting style approximates the Visual Studio Classic light theme.
- Avoid switching the default template to `minted` unless the user accepts the Python/Pygments dependency and shell escape requirement.

## Test Case Blocks

- Use `mzTestCaseBlock` for Word-style test case content blocks that contain `测试步骤`、`预期结果`、`实际运行结果`、`测试结论`.
- Use `\mzTestBlockTitle{测试步骤}` and similar titles inside `mzTestCaseBlock`; it renders a black square, blank spacing, and bold title text. Do not reintroduce an arrow after the square unless the user explicitly asks.
- Put numbered steps in ordinary `enumerate` lists inside `mzTestCaseBlock`; the environment keeps list spacing compact and aligns the numeric labels with the block title prefix.
- `mzTestCaseBlock` applies a `2em` left indent to mimic a Word Tab before the whole block.
- Use `\mzQuotedCode{/path/}` for quoted inline code/path fragments that must render with straight ASCII double quotes, for example `"/ymounterr/"`.
- These helpers are defined in `styles/report-style.sty` and should be reused instead of hard-coding spacing in individual chapters.

## Report Tables

- Use `mzTable` around report data tables, especially tables imported from Word.
- `mzTable` is defined in `styles/report-style.sty`; it applies compact table font sizing, controlled row spacing, and black rules to match the old formal report more closely.
- Use `mzCompactTable` for dense numeric tables that would otherwise feel oversized or force awkward header wrapping.
- Prefer stable report-style grid tables over decorative modern tables. Avoid gray striping unless the user explicitly asks for it.
- For formal grid tables, keep all rules as single black lines. Do not stack consecutive `\hline` commands; two adjacent `\hline` commands render as a visibly thicker rule and make table line weights inconsistent.
- When converting Word tables to LaTeX grid tables, use vertical bars in the column specification only when full Word-style borders are desired, and use one `\hline` at the table top and one after each row.
- If a table uses `longtable` continuation heads or footers, apply the same single-line rule discipline in `\endfirsthead`, `\endhead`, `\endfoot`, and `\endlastfoot`.
- Before finalizing broad table restyling, search all chapters for repeated `\hline` and mixed table-rule commands, then render the PDF and inspect every table page visually. Source-level checks alone are not enough for line-weight issues.
- Avoid mixing `booktabs` rules (`\toprule`, `\midrule`, `\bottomrule`) with full grid `\hline` rules in the same table unless the user explicitly asks for a different table style.
- Split overloaded Word tables into several semantic LaTeX tables when a single imported table mixes unrelated measurements or becomes too wide.

## Git Hygiene

- Preserve user changes. Do not revert files unless explicitly asked.
- `output/` is local build output and should remain untracked.
- Before finalizing, check `git status --short` and report source files changed.

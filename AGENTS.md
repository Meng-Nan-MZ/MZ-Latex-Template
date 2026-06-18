# Agent Notes

This file records project-specific conventions for AI agents and collaborators. Keep user-facing documentation in `README.md`; use this file for workflow memory and maintenance rules.

## Scope

- Work primarily inside this `MZ-Latex-Template` project.
- Treat sibling folders such as `REF/` as reference material unless the user explicitly asks to modify them.
- Keep edits focused on the requested template behavior. Avoid unrelated rewrites or style churn.

## Build

- Compile locally with XeLaTeX from the project root:

```powershell
xelatex -interaction=nonstopmode -halt-on-error -output-directory=output main.tex
xelatex -interaction=nonstopmode -halt-on-error -output-directory=output main.tex
```

- The second run refreshes the table of contents and cross references.
- Keep the local `output/` directory. It is intentionally ignored by Git through `.gitignore`.
- Do not delete `output/` just to clean status unless the user explicitly asks.

## LaTeX Style

- Global packages and reusable environments belong in `styles/report-style.sty`.
- Chapter examples and document content belong in `chapters/*.tex`.
- The template uses `ctexrep` with XeLaTeX and `fontset=fandol`; avoid changes that require unavailable system fonts unless requested.
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
- Use `\mzTestBlockTitle{测试步骤}` and similar titles inside `mzTestCaseBlock`; it renders the black square plus arrow prefix used by the source Word document.
- Put numbered steps in ordinary `enumerate` lists inside `mzTestCaseBlock`; the environment keeps list spacing compact and aligns the numeric labels with the block title prefix.
- `mzTestCaseBlock` applies a `2em` left indent to mimic a Word Tab before the whole block.
- Use `\mzQuotedCode{/path/}` for quoted inline code/path fragments that must render with straight ASCII double quotes, for example `"/ymounterr/"`.
- These helpers are defined in `styles/report-style.sty` and should be reused instead of hard-coding spacing in individual chapters.

## Report Tables

- Use `mzTable` around report data tables, especially tables imported from Word.
- `mzTable` is defined in `styles/report-style.sty`; it applies compact table font sizing, controlled row spacing, muted alternating row backgrounds, and booktabs-compatible rule colors.
- Prefer `booktabs` rules (`\toprule`, `\midrule`, `\bottomrule`) instead of full grid `\hline` tables.
- Avoid vertical rules in column specifications unless the user explicitly asks for Word-style grid borders.
- Split overloaded Word tables into several semantic LaTeX tables when a single imported table mixes unrelated measurements or becomes too wide.

## Git Hygiene

- Preserve user changes. Do not revert files unless explicitly asked.
- `output/` is local build output and should remain untracked.
- Before finalizing, check `git status --short` and report source files changed.

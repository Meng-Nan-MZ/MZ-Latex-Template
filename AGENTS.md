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

## Git Hygiene

- Preserve user changes. Do not revert files unless explicitly asked.
- `output/` is local build output and should remain untracked.
- Before finalizing, check `git status --short` and report source files changed.

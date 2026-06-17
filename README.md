# YAFFS report LaTeX project

## File roles

- `main.tex`: document entry point. It controls the document order only: cover pages, table of contents, chapters, and appendix.
- `styles/report-style.sty`: global style file. It controls page geometry, packages, fonts inherited from `ctexrep`, chapter/section styles, table of contents style, caption style, numbering depth, and page footer.
- `chapters/cover_pages.tex`: cover and signature pages.
- `chapters/meta.tex`: reusable report metadata macros.
- `chapters/cha01.tex` to `chapters/cha04.tex`: main chapter files.
- `chapters/appendix.tex`: appendix file.
- `figures/`: project figures used by the current report.
- `REF/`: reference material. It is not compiled by the current report.
- `output/`: local build output. It is not required by Overleaf.

## Local compile

Use XeLaTeX:

```bash
xelatex -interaction=nonstopmode -halt-on-error -output-directory=output main.tex
xelatex -interaction=nonstopmode -halt-on-error -output-directory=output main.tex
```

The second run refreshes the table of contents and cross references.

## Overleaf

Set the compiler to `XeLaTeX`.

For basic Overleaf compatibility, upload:

- `main.tex`
- `styles/`
- `chapters/`
- `figures/`

Do not upload `output/` or local temporary files.

The current project uses `ctexrep` with `fontset=fandol`, so local Windows builds and Overleaf builds use the same CTEX bundled Chinese font family. This makes the output closer across platforms. If identical Word-like SimSun output is required, fonts must be explicitly configured and legally available to the project.

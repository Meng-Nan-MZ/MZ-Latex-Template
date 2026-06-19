# Bundled Fonts

Put the licensed font files used by projects based on this template in this folder before exporting to Overleaf.

Expected file names:

- `simsun.ttc`: Chinese SimSun / Songti body font.
- `times.ttf`: Times New Roman regular.
- `timesbd.ttf`: Times New Roman bold.
- `timesi.ttf`: Times New Roman italic.
- `timesbi.ttf`: Times New Roman bold italic.

Do not rename these files unless you also update `styles/report-style.sty`.

When these files are present, local XeLaTeX and Overleaf XeLaTeX load the same font files from this folder. If they are absent, the template falls back to system font names for local editing, which may fail on Overleaf when the font is not installed there.

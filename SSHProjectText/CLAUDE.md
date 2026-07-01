# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this directory is

A LaTeX learning/editing sandbox built from a reference paper (`VITALflow_2022.pdf`, an IEEE conference
paper on network traffic visualization). `skeleton.tex` mirrors that paper's section structure
(Introduction, Related Work, Typical Tasks and Requirements, Approach with subsections, Implementation,
Evaluation and Discussion, Summary, Acknowledgments) but every section body is Lorem Ipsum placeholder
text generated via the `lipsum` package, and two generated placeholder images stand in for real figures.
The goal is to let the user learn/experiment with LaTeX syntax against a realistic paper skeleton, not to
reproduce the actual paper content.

## Build commands

The file has a bibliography (`refs.bib`), so a full build needs 4 passes — pdflatex, bibtex, then
pdflatex twice more to resolve citation numbers:

```
pdflatex -interaction=nonstopmode skeleton.tex
bibtex skeleton
pdflatex -interaction=nonstopmode skeleton.tex
pdflatex -interaction=nonstopmode skeleton.tex
```

Or just use `latexmk`, which figures out how many passes are needed automatically:

```
latexmk -pdf -interaction=nonstopmode skeleton.tex
```

This produces `skeleton.pdf`. Clean up aux files after building:

```
rm -f skeleton.aux skeleton.log skeleton.out skeleton.bbl skeleton.blg skeleton.fdb_latexmk skeleton.fls
```

Alternatively, open `skeleton.tex` in VS Code (LaTeX Workshop extension is installed, backed by
`latexmk`) — it auto-builds on save and shows the rendered PDF in a side tab (see `.vscode/settings.json`).

## Structure notes

- Section numbering is overridden to Roman numerals (`\thesection` → `\Roman{section}`) to mirror the
  IEEE-style look of the source paper, since the `IEEEtran` document class itself is not installed in
  this environment — the skeleton uses plain `article` with `twocolumn` instead.
- Figures reference `placeholder1.png` and `placeholder2.png` (generated with Pillow) at different
  `\includegraphics` widths, intentionally, to show how image scaling works.
- `refs.bib` holds real published-paper entries (citation keys, not full content) used to demonstrate
  `\cite{}` in Introduction/Related Work/Approach, with `ieeetr` bibliography style (numbered brackets,
  matching the source paper's citation look). BibTeX treats any `@` character as a new-entry marker,
  even inside a `%` comment — don't type `@` in `refs.bib` comments, or parsing breaks.
- Every non-obvious LaTeX command in `skeleton.tex` has an inline comment explaining what it does —
  keep that pattern when adding new constructs, since the file's purpose is pedagogical.

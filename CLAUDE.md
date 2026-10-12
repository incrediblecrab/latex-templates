# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) and GitHub Copilot CLI when working in this repository.

Two standalone pdfLaTeX research-paper templates, `single-column.tex` and `double-column.tex`, each with a committed preview PDF. The repository is public. Each `.tex` file is self-contained on purpose: the two repeat their shared styling so either can be copied alone, with no class file, style file, bibliography or image asset. Keep it that way rather than factoring the styling out.

## Commands

```bash
latexmk -pdf -interaction=nonstopmode -halt-on-error -outdir=build single-column.tex
latexmk -pdf -interaction=nonstopmode -halt-on-error -outdir=build double-column.tex
```

After editing a template, copy its PDF from `build/` to the repository root and commit it with the source so the preview matches; never commit `build/` or auxiliary files. No shell escape, BibTeX or Biber is used.

## Rules

The templates' inline comments are the instructions an LLM follows when filling one in, so keep them accurate whenever the layout changes. The double-column template uses native `\twocolumn[...]`, never `multicols`, and body floats use `\linewidth`. Citations are linked footnotes, not a bibliography; example URLs and all `\lipsum` text are placeholders. Palatino (`mathpazo`) is enabled by default and commenting out that one line restores the default font. The `README.md` "Layout and safe changes" table is the reference for supported edits.

This repository is also checked out as the `templates/` submodule of `barycenter-wiki`, which lists these files; a rename or a new template changes what that site shows the next time its submodule is updated.

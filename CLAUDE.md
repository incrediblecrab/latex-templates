# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) and GitHub Copilot CLI when working in this repository.

Two standalone pdfLaTeX templates, each with a committed preview PDF: the research papers `single-column.tex` and `double-column.tex`. This is the one home for the owner's LaTeX templates, and the repository is public, so templates hold placeholders only, never personal details. Each `.tex` file is self-contained on purpose: the two paper templates repeat their shared styling so either can be copied alone, with no class file, style file, bibliography or image asset. Keep it that way rather than factoring the styling out.

## Commands

```bash
latexmk -pdf -interaction=nonstopmode -halt-on-error -outdir=build single-column.tex
latexmk -pdf -interaction=nonstopmode -halt-on-error -outdir=build double-column.tex
```

After editing a template, copy its PDF from `build/` to the repository root and commit it with the source so the preview matches; never commit `build/` or auxiliary files. No shell escape, BibTeX or Biber is used.

## Rules

The templates' inline comments are the instructions an LLM follows when filling one in, so keep them accurate whenever the layout changes. The double-column template uses native `\twocolumn[...]`, never `multicols`, and body floats use `\linewidth`. Citations are linked footnotes, not a bibliography; example URLs and all `\lipsum` text are placeholders. Computer Modern is the default, loaded through `lmodern` because `T1` encoding otherwise falls back to bitmap fonts; Palatino (`mathpazo`) is commented out beside it, and swapping the two lines switches fonts. The `README.md` "Layout and safe changes" table is the reference for supported edits.

This repository is also checked out as the `templates/` submodule of `barycenter-wiki`, which lists these files; a rename or a new template changes what that site shows the next time its submodule is updated.

# LaTeX templates

Two standalone research-paper templates with lorem ipsum filler and inline
instructions for LLM-assisted editing. Each file is a complete document: no
custom class, shared style file, bibliography, image, or build configuration
is required.

| File | Layout |
| --- | --- |
| [`single-column.tex`](single-column.tex) | One column throughout, with an inline title and abstract. |
| [`double-column.tex`](double-column.tex) | Full-width title and abstract above a two-column body. |

Both include a linked footnote, an asset-free figure placeholder, a wrapping
table, a list, and back matter. All sample prose is filler, not research.
The two files intentionally repeat their shared styling so either can be used
independently.

## Build

Use **pdfLaTeX** with a current TeX Live, MacTeX, or MiKTeX installation.
`latexmk` is recommended because it reruns LaTeX to resolve figure/table
references and the total page count.

Run either command from the directory containing the chosen template:

```sh
latexmk -pdf -interaction=nonstopmode -halt-on-error -outdir=build single-column.tex
latexmk -pdf -interaction=nonstopmode -halt-on-error -outdir=build double-column.tex
```

The corresponding PDF and auxiliary files go in `build/`. No `.latexmkrc`
is needed. Keep generated files out of source commits.

Without `latexmk`, run pdfLaTeX twice (substitute the other filename as needed):

```sh
mkdir -p build
pdflatex -interaction=nonstopmode -halt-on-error -output-directory=build single-column.tex
pdflatex -interaction=nonstopmode -halt-on-error -output-directory=build single-column.tex
```

If references still request another pass, rerun until they settle. On Overleaf,
upload either `.tex` file, select it as the main document, and choose pdfLaTeX.

All packages are supplied by standard TeX distributions. Minimal installations
may need additional packages; the preamble lists them explicitly. In particular,
the templates use `mathpazo` (for Palatino), `microtype`, `parskip`, `titlesec`, `enumitem`,
`caption`, `booktabs`, `tabularx`, `fancyhdr`, `lastpage`, `xurl`, and `lipsum`.
No system-font installation, shell escape, BibTeX, or Biber is needed.

## Font choice

Choose **LaTeX default (Computer Modern)** or **Palatino**. Both templates
have Palatino enabled. To use the default font instead, comment out this
line in the chosen `.tex` file:

```latex
% \usepackage{mathpazo}
```

Uncomment it to restore Palatino. This switches both text and math fonts;
leave the encoding and language packages unchanged. No other font package
or compilation engine is needed.

## Use with an LLM

Give the LLM the **entire chosen `.tex` file**, your brief, and the source
material. The inline comments explain which text to replace and which layout
mechanics to preserve. A starting prompt:

```text
Use the attached LaTeX template to write a paper from my brief and sources.
Read its comments first. Keep the existing typography and column layout.
Replace the metadata, all lorem ipsum, and every example URL or label.
Use only supported facts and real sources; identify missing information
rather than inventing it. Keep the document self-contained unless I supply
external assets. Return the complete edited .tex file.
```

Edit `\PaperTitle`, `\PaperAuthor`, `\PaperDate`, `\PaperAbstract`, and
`\PaperKeywords` near the top. Title, author, and keywords are reused in the
PDF metadata. Replace every `\lipsum[...]` call and the literal Latin text,
including subsection headings, captions, table cells, and back matter.
Replace `Month Year` with an explicit publication date.

The default structure is **introduction, context and stakes, core analysis,
implications, conclusion**, followed by a glossary, about section, and
disclosure. Introduction and conclusion are unnumbered; the three support
sections each have two example subsections. Use two introductory paragraphs
to establish the question and framework, and two concluding paragraphs to
answer it and state what would falsify the conclusion. Keep headings in
sentence case, the title at most 55 characters, the abstract at most three
sentences, and keywords to four to six terms.

Citations use linked footnotes rather than a separate bibliography:

```latex
\footnote{\href{https://example.com/}{Publisher, Month Day, Year.}}
```

That URL is a placeholder, not a source. Supply the actual URL, publisher,
and date; consolidate same-source facts within a paragraph into one trailing
footnote. Keep citations in the body, not the title, abstract, or PDF metadata.
Do not treat the disclosure filler as a legal disclaimer or a declaration
about the author's interests.

## Layout and safe changes

The shared style uses **11pt type** in the chosen font, US letter paper, 0.5in top/side
margins, a 0.75in bottom margin, 1.15 line spacing, unindented paragraphs,
compact lists, black hyperlinks, and a gray `page / total` footer. The
two-column version has a 0.5in gutter. Both start the paper on the title page
rather than adding a separate cover sheet.

The double-column template uses native `\twocolumn[...]`, not `multicols`.
Its bracketed opening spans the page; everything after it flows into columns.
Do not mix the two column systems or switch to `\onecolumn` just to insert
a wide object.

| Task | Approach |
| --- | --- |
| Add an image | Replace the whole example `\fbox` with `\includegraphics[width=\linewidth]{figure.pdf}` after supplying that file. |
| Fit a normal figure/table | Use `\linewidth`, the available local width. In two-column body floats, `\textwidth` is too wide. |
| Span both columns | Use `figure*` or `table*` with `[t]`, changing both the opening and closing environment names. These normally appear at the top of a later page. |
| Refer to a figure/table | Put `\label` after `\caption`; use `\ref` instead of hard-coded numbers. Update or remove matching references when deleting examples. |
| Start a fresh appendix page | Use `\clearpage`, which flushes pending floats. In two-column mode, `\newpage` only starts the next column. |
| Handle overflow | Shorten headings, wrap table columns, or use a wide float. Keep normal hyphenation and visible warnings; avoid tiny type and negative-spacing patches. |

Figure and table placement is intentionally flexible, not fixed to a line.
The last two-column page is not automatically balanced. Review the PDF after
replacing the filler for clipped text, awkward breaks, misplaced floats,
unresolved references, and leftover placeholders.

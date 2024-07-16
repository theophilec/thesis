# My PhD Thesis

Author: Théophile CANTELOBRE
Supervisors : Benjamin GUEDJ, Alessandro RUDI and Carlo CILIBERTO.

## Building the file using MacOS
In the `.latexmkrc` file, include:
```
$pdf_previewer = 'open -a Skim';
$pdflatex = 'pdflatex -synctex=1 -interaction=nonstopmode';
@generated_exts = (@generated_exts, 'synctex.gz');
```
Then, run `latexmk -pdf -pvc -interaction=nonstopmode main.tex` in a Terminal.

I wasn't able to get `synctex` working with Zed though.

## Tips and tricks for future PhD students

- Use a single growing `.bib` file, for example from a bibliography management tool like Zotero. Concatenating `.bib` files is a pain (duplicate entries, ...).
- Use a single growing `macro.sty` file. This can be hard because journal and conference templates vary.
- Prepare a "vanilla" formatted edition of each paper / draft to make integration easier when writing your PhD.

## Some Latex learnings
- Using  `babel` for French messes with the `sec:section-name` convention I use because of the `:` while outputting cryptic error messages...
- For some reason `'` (single quotes) are not handled in math-mode with this template.
- `latexmk` does not watch files that are 2 inputs in, i.e. `main.tex` has an `\input(a)` and `a` has an `\input(b)` then `b` is not watched by `latexmk`.

## Template
Template proposed by Arthur Chavignon (2022) based on a template by [Pierre Guillou](https://pierre.guillou.net/psl-cover/2018/) (Version 1.2 (20 juillet 2019)) with PSL cover page.
I downloaded it from Overleaf.

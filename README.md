# tikz2svg

`tikz2svg` is a simple Bash script for converting TikZ code to SVGs.

## Usage

```shell
tikz2svg <FILE> [<FILE2> ...]
tikz2svg *.tex
```

## Inner Workings

This is very much a utility wrapper script around `pdflatex` and `pdf2svg`.
You will need to have these installed for this to work.

`tikz2svg` wraps the content of the passed files in a `circuitikz` environment, so **files should *only* contain TikZ code**.
The full structure of the file is given below.

```latex
\documentclass[margin=1mm]{standalone}

\usepackage{xcolor}
\definecolor{backgroundcolour}{rgb}{240, 240, 240}

\usepackage{circuitikz}
\usetikzlibrary{arrows.meta}

\usepackage{pagecolor}

\begin{document}
\pagecolor{backgroundcolour}
\begin{circuitikz}[european]

% +------------------------------+
% |     passed file contents     |
% +------------------------------+

\end{circuitikz}
\end{document}
```

## Pitfalls

This is not a particularly intelligent script - the one thing it really checks is that the file you just passed actually exists.
If the compilation fails, `pdflatex` will simply block execution.
In this case, it's best to review the log (which won't've been cleaned up), since `pdflatex` just shut down and refused to accept inputs from anyone (including `^C`).
This can be found at `TEMPORARY_tikz2svg_intermediate.log`, and the error will be right at the bottom.

## Useful Commands LateX edition
Adding here useful LateX commands I find myself forgetting and having to routinely google or look up in my own scripts.

Mostly, I figured these out when compiling my [PhD thesis](https://github.com/annacuomo/PhD_Thesis/).

* ```\clearpage``` instead of ```\newpage```, when figures and tables just move around and don't stay where you put them, this is a good way to enforce an order ([for example, to enforce the caption of Fig S2 to go after the figure](https://github.com/annacuomo/CellRegMap_Supplementary_Methods/blob/main/supplementary_figures.tex)).
* ```\textcolor{blue}{text_i_need_in_colour}``` to colour one piece of text (_e.g._, minor revisions for my thesis)
* in formulae, ```\in``` is the "belongs to" symbol
* ```\leq``` smaller or equal
* to capitalise greek letters, use ```\boldsymbol{\theta}```
* in formulae, ```sim``` is ~ (distributed as)
* ```\underbrace_{y}_{sc. \ expr}``` adds an bracket under ```y``` to specify it represents single-cell expression

To write a system of equations, ```\usepackage{systeme}``` in main and then 
```
\systeme{
    part1,
    part2
    },
```
For tables with multi-row captions, ```\usepackage{multirow}``` in main and then, _e.g.,_ ([Box on confusion matrix from {hD thesis](https://github.com/annacuomo/PhD_Thesis/blob/main/Chapter2/chapter2.tex#L231-L242)):
```
\begin{center}
\begin{tabular}{l|l|c|c|}
\multicolumn{2}{c}{}&\multicolumn{2}{c}{Test Result}\\
\cline{3-4}
\multicolumn{2}{c|}{}&reject $H_0$&accept $H_0$\\
\cline{2-4}
\multirow{2}{*}{Actual value}& $H_1$ & True Positive ($TP$) & False Negative ($FN$)\\
\cline{2-4}
& $H_0$ & False Positive ($FP$) & True Negative ($TN$)\\
\cline{2-4}
\end{tabular}
\end{center}
```

## Resources

* https://www.geeksforgeeks.org/logic-notations-in-latex/
* https://oeis.org/wiki/List_of_LaTeX_mathematical_symbols

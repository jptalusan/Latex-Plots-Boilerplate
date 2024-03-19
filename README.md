# Latex Plotting Boilerplate

This is a working Latex template for drawing plots and simple charts using pgfplot and tikz.

## Basic Use

Most basic plot needs the following packages:
```latex
\usepackage{graphicx} % Required for inserting images
\usepackage{pgfplots}
\usepackage{pgfplotstable}
\usepgfplotslibrary{statistics}
\pgfplotsset{compat=1.18}
```

Version `1.18`` is currently the latest version for pgfplots listed [here](https://ctan.org/pkg/pgfplots?lang=en).

To import your own CSV, upload it to the Overleaf directory and load it using:

```latex
\pgfplotstableread[col sep=comma]{data/data.csv}\csvdata
```
This means you have read a comma separated CSV file inside `data/` folder and have given it the variable name `\cscvdata`.

To plot a simple line plot:

```latex

\begin{figure}
\centering
\begin{tikzpicture}
    \begin{axis}[
        xtick=data,
        xticklabels from table={\loadedtable}{COUNT},
    ]
        \addplot[no marks, 
                 thick, 
                color=red!100] 
            table[
                x=Day, 
                y=Value, 
                col sep=comma]
            {\csvdata};
        \legend{Value}
    \end{axis}
\end{tikzpicture}
\caption{Bar Plot From CSV}
\end{figure}
```

`\addplot` controls the plot to be added with the parameters inside `[]` controlling how the plot is drawn. Meanwhile, `table[]` controls the data to be added into the plot. Finally, `{\csvdata}` informs the table where the data is going to come from.

Adjusting the dimensions and characteristics of the main plot is controlled in `\begin{axis}[...]`. Here, you can modify the height, width, plot type, legend position, style, labels, and more.

## Contents of the boilerplate
Each one of the `.tex` files listed here corresponds to a single plot. Note that you will definitely have to preprocess your results before using them with these plots.

```latex
\input{plots/one_boxplot}
% Simple box plot for a single dataset with 5 xtick labels.

\input{plots/color_boxplot}
% A different way to use box plots. I think it's hard to plot box plots using TikZ.

\input{plots/bar_with_errors}
% Bar plots with the data added in-line or within the code. This features 2 sets of bars per x-axis.

\input{plots/bar_with_errors_from_file}
% Same as above, except this one reads from a file.

\input{plots/bar_read_csv}
% Simple bar plots without error bars.

\input{plots/lineplot}
% Simple line plot (2 sets of lines here). Features use of `xtick distance`

\input{plots/marker_plus_line}
% Two sets of plots, one a line plot and another a scatter plot in the same axis.

\input{plots/heatmap}
% Heatmap, aside from box plots, i think TikZ has difficulty with heatmaps. This uses some programming tools inside latex such as For loops.

\input{plots/two_boxplots}
% Similar to the 2 sets of bar plots, this is for box plots. Note how the data is processed and used: Using `mean` and `error` data. But preprocessing can be done in Latex if needed (beyond the scope of this tutorial, see bar_read_csv.tex).

\input{plots/multiple_subplots}
% Several examples of using groupplots to plot subplots (multiple cols, multiple rows, and a 2-D subplot)

\input{plots/two_y_axes}
% Simple example using two y-axis plots and the legends are joined in a single legend.

\input{plots/filter}
% Uses the `filter./code` function to filter specific aspects of the datasets. Can filter strings too.

\input{plots/restricting}
% Uses `restrict expr to domain` to filter specific rows inside the data. Can be used in sequence. Note, this only works with numerical values.

\input{plots/fillbetween}
% For use when you want to color a specific part between two curves. This shows a fill between the x-axis and the main curve. `soft clip` controls the area.

\input{plots/heatmap_v2}
% Heatmap version 2. I think this shows more promise. Again, this uses some programming tools inside latex such as For loops. Font inside is controlled within `node`

\input{charts/basic_flowchart}
% Creating flowcharts using Latex, easier to adjust and more readable than Draw.io figures.
```

## References
1. [Manual for PGFplots](https://tikz.dev/pgfplots/)
2. [Tutorial for Drawing/Creating Flowcharts using TikZ](https://www.overleaf.com/learn/latex/LaTeX_Graphics_using_TikZ%3A_A_Tutorial_for_Beginners_(Part_3)%E2%80%94Creating_Flowcharts)
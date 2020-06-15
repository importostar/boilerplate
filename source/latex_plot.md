---
title: latex_plot
date: 2020-05-07
---
Example Python program latex_plot.py

## Modules

* import matplotlib as mpl
* import matplotlib.pyplot as plt

## Code

Python example

    # Copied from http://nasseralkmim.github.io/notes/2017/02/28/consistent-typeface-between-matplotlib-plot-and-latex/
    import matplotlib as mpl
    import matplotlib.pyplot as plt
    
    pgf_with_latex = {
        # # LaTeX default is 10pt font.
        "text.usetex": True,
        # # setup matplotlib to use latex for output
        "pgf.texsystem": "xelatex",
        # use LaTeX to write all text
        'text.latex.unicode': True,
        "font.family": "DejaVu Sans",
        "font.serif": [],
        # # blank entries should cause plots to inherit fonts from the document
        # "font.sans-serif": [],
        # "font.monospace": [],
        'path.simplify': True,
        'path.simplify_threshold': 0.1,
        'legend.markerscale': .9,
        'legend.numpoints': 1,
        'legend.handlelength': 2,
        'legend.scatterpoints': 1,
        'legend.labelspacing': 0.5,
        'legend.facecolor': '#eff0f1',
        'legend.edgecolor': 'none',
        'legend.handletextpad': 0.5,  # pad between handle and text
        'legend.borderaxespad': 0.5,  # pad between legend and axes
        'legend.borderpad': 0.5,  # pad between legend and legend content
        'legend.columnspacing': 1,  # pad between each legend column
        'axes.spines.left': True,
        'axes.spines.top': True,
        'axes.titlesize': 'large',
        'axes.spines.bottom': True,
        'axes.spines.right': True,
        'axes.axisbelow': True,
        'axes.grid': True,
        'image.cmap': 'RdYlBu',
        'grid.linewidth': 0.5,
        'grid.linestyle': '-',
        'grid.alpha': .6,
        'lines.linewidth': 1,
        'lines.markersize': 4,
        'lines.markeredgewidth': 1,
        'pgf.preamble': [
            r'\usepackage[utf8x]{inputenc}',
            r'\usepackage[T1]{fontenc}',
            r'\usepackage{{{typeface}}}'
        ]
    }
    mpl.rcParams.update(pgf_with_latex)
    
    f, ax = plt.subplots(figsize=(12, 3))
    ax.plot(list(range(5)))
    f.savefig('img1.pdf', bbox_inches='tight')

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

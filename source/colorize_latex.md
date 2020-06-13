---
title: colorize_latex
date: 2020-05-07
---
Example Python program colorize_latex.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import numpy as np
* import matplotlib
* import matplotlib.pyplot as plt

## Methods

* def latex_colorize(text, weights):

## Code

Python example

    import numpy as np
    import matplotlib
    matplotlib.use('Agg')
    import matplotlib.pyplot as plt
    
    color_name = 'color{}'
    define_color = '\definecolor{{{}}}{{HTML}}{{{}}}'
    box = '\\mybox{{{}}}{{\strut{{{}}}}}'
    
    cmap = plt.cm.get_cmap('RdBu')
    for i, x in enumerate(np.arange(0, 1, 0.1)):
        rgb = matplotlib.colors.rgb2hex(cmap(x)[:3])
        print(define_color.format(color_name.format(i), rgb[1:]))
    
    print()
    print('''\\newcommand*{\mybox}[2]{\\tikz[anchor=base,baseline=0pt] \\node[fill=#1!60!white] (X) {#2};}''')
    print()
    
    def latex_colorize(text, weights):
        s = ''
        for w, x in zip(text, weights):
            color = np.digitize(x, np.arange(0, 1, 0.1)) - 1
            s += ' ' + box.format(color_name.format(color), w)
        return s
    
    text = "What company won a free advertisement due to the QuickBooks contest ?".split()
    weights = [0.1, 0.0, 0.0, 0.8, 0.9, 0.4, 0.2, 0.2, 0.1, 0.4, 0.5, 0.6]
    assert len(text) == len(weights)
    print('\\footnotesize', latex_colorize(text, weights))

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

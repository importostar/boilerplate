---
title: latexify
date: 2020-05-07
---
Example Python program latexify.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import pandas as pd
* import matplotlib
*   import mpld3

## Methods

* def latexify(fig_width=None, fig_height=None, columns=1, max_height_inches=8.0):

## Code

Python example

    %matplotlib inline
    import pandas as pd
    import matplotlib
    try:
      import mpld3
    except:
      pass
    
    def latexify(fig_width=None, fig_height=None, columns=1, max_height_inches=8.0):
        """Set up matplotlib's RC params for LaTeX plotting.
        Call this before plotting a figure.
    
        Parameters
        ----------
        fig_width : float, optional, inches
        fig_height : float,  optional, inches
        columns : {1, 2}
        """
    
        # code adapted from http://www.scipy.org/Cookbook/Matplotlib/LaTeX_Examples
    
        # Width and max height in inches for IEEE journals taken from
        # computer.org/cms/Computer.org/Journal%20templates/transactions_art_guide.pdf
    
        assert(columns in [1,2])
    
        if fig_width is None:
            fig_width = 3.39 if columns==1 else 6.9 # width in inches
    
        if fig_height is None:
            golden_mean = (np.sqrt(5)-1.0)/2.0    # Aesthetic ratio
            fig_height = fig_width*golden_mean # height in inches
    
        if fig_height > max_height_inches:
            print("WARNING: fig_height too large:" + fig_height + 
                  "so will reduce to" + max_height_inches + "inches.")
            fig_height = max_height_inches
    
        params = {'backend': 'ps',
                  'text.latex.preamble': [r'\usepackage{gensymb}'],
                  'axes.labelsize': 8, # fontsize for x and y labels (was 10)
                  'axes.titlesize': 8,
                  'text.fontsize': 8, # was 10
                  'legend.fontsize': 8, # was 10
                  'xtick.labelsize': 8,
                  'ytick.labelsize': 8,
                  'text.usetex': True,
                  'figure.figsize': [fig_width,fig_height],
                  'font.family': 'serif'
        }
    
        matplotlib.rcParams.update(params)

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

---
title: notebook visualization
date: 2020-05-07
---
Example Python program notebook-visualization.py

## Modules

* from glob import glob
* import os
* import matplotlib as mpl
* from matplotlib.colors import ListedColormap
* import matplotlib.pyplot as plt
* import numpy as np
* import pandas as pd
* import seaborn as sns

## Code

Python example

    ## Cell 1
    from glob import glob
    import os
    
    import matplotlib as mpl
    from matplotlib.colors import ListedColormap
    import matplotlib.pyplot as plt
    import numpy as np
    import pandas as pd
    import seaborn as sns
    
    %matplotlib inline
    %config InlineBackend.figure_format='retina'
    
    CMAP = ListedColormap(sns.color_palette('RdBu_r', 16))
    pd.set_option('display.max_columns', None)
    
    # ==================================
    
    ## Cell 2
    plt.style.use('fivethirtyeight')
    sns.set_style('white', {'axes.grid': True})
    mpl.rcParams['figure.figsize'] = (10, 6)
    mpl.rcParams['image.cmap'] = 'coolwarm'
    mpl.rcParams['font.family'] = 'sans-serif'
    mpl.rcParams['font.size'] = 22
    mpl.rcParams['text.usetex'] = False
    mpl.rcParams['savefig.dpi'] = 240
    mpl.rcParams['savefig.facecolor'] = 'white'
    mpl.rcParams['savefig.bbox'] = 'tight'
    
    ## Colors
    greys = ['#4a4a49', '#6e6e6d', '#9b9b9b', '#c4c5c5', '#e2e2e2']
    greens = ['#007844', '#5ca551', '#218c55', '#67b785', '#8cd8a8']
    blues = ['#0005ad', '#297bbb', '#4e98d2', '#64b0da', '#80c6ec']
    yellow = '#ffdd00'
    orange = '#f7a600'
    darkorange = '#ef7c00'
    
    grey = greys[1]
    green = greens[1]
    blue = blues[1]

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

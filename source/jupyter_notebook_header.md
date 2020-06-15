---
title: jupyter_notebook_header
date: 2020-05-07
---
Example Python program jupyter_notebook_header.py

## Modules

* import numpy as np
* import pandas as pd
* from pandas import DataFrame, Series
* import warnings
* from scipy import signal, stats
* from statsmodels.nonparametric.smoothers_lowess import lowess
* from sklearn.decomposition import PCA
* from IPython.display import set_matplotlib_formats
* import matplotlib
* import matplotlib.pyplot as plt
* from matplotlib.colors import ListedColormap
* from matplotlib.patches import Rectangle
* from matplotlib.lines import Line2D
* import mpld3
* import seaborn as sns

## Methods

* def abline(slope, intercept, ax=None):
* def add_lowess(x, y, ax=None, color=None, is_sorted=True, frac=0.005, it=0, **kwargs):
* def add_band(x_low, x_high, y_low=None, y_high=None, ax=None, color='gray', linewidth=0, alpha=0.5, zorder=0, **kwargs):
* def stairs(df, start='start', end='end', pos='pos', endtrim=0):
* def pca(matrix, labels=None, n_components=2):

## Code

Python example

    %matplotlib inline
    
    import numpy as np
    import pandas as pd
    from pandas import DataFrame, Series
    import warnings
    from scipy import signal, stats
    from statsmodels.nonparametric.smoothers_lowess import lowess
    from sklearn.decomposition import PCA
    
    # Make inline plots vector graphics instead of raster graphics
    from IPython.display import set_matplotlib_formats
    #set_matplotlib_formats('pdf', 'svg')
    set_matplotlib_formats('retina', 'png')
    
    import matplotlib
    import matplotlib.pyplot as plt
    from matplotlib.colors import ListedColormap
    from matplotlib.patches import Rectangle
    from matplotlib.lines import Line2D
    
    #matplotlib.rcParams['figure.figsize'] = (20.0, 10.0)
    
    import mpld3
    
    import seaborn as sns
    sns.set() # sets seaborn default "prettyness:
    sns.set_style("white")
    sns.set_context("notebook")
    
    def abline(slope, intercept, ax=None):
        "Add a straight line through the plot"
        if ax is None:
            ax = plt.gca()
        x_vals = np.array(ax.get_xlim())
        y_vals = intercept + slope * x_vals
        ax.plot(x_vals, y_vals, '--', color='grey')
        
    def add_lowess(x, y, ax=None, color=None, is_sorted=True, frac=0.005, it=0, **kwargs):
        "Add a lowess curve to the plot"
        if ax is None:
            ax = plt.gca() 
        filtered = lowess(y, x, is_sorted=is_sorted, frac=frac, it=it, **kwargs)
        ax.plot(filtered[:,0], filtered[:,1])
    
    def add_band(x_low, x_high, y_low=None, y_high=None, ax=None, color='gray', linewidth=0, alpha=0.5, zorder=0, **kwargs):
        "Plot a gray block on x interval"
        if ax is None:
            ax = plt.gca()
        if y_low is None:
            y_low, _ = ax.get_ylim()
        if y_high is None:
            _, y_high = ax.get_ylim()
        g = ax.add_patch(Rectangle((x_low, y_low), x_high-x_low, y_high-y_low, 
                     facecolor=color,
                     linewidth=linewidth,
                     alpha=alpha,
                     zorder=zorder,
                     **kwargs))
    
    def stairs(df, start='start', end='end', pos='pos', endtrim=0):
        "Turn a df with start, end into one with pos to plot as stairs"
        df1 = df.copy(deep=True)
        df2 = df.copy(deep=True)
        df1[pos] = df1[start]
        df2[pos] = df2[end] - endtrim
        return pd.concat([df1, df2]).sort_values([start, end])
    
    # My own paired palette replacing the last brown pair with violets
    sns.color_palette('Paired').as_hex()
    Paired = sns.color_palette(['#a6cee3', '#1f78b4', '#b2df8a', '#33a02c', '#fb9a99', '#e31a1c',
                                '#fdbf6f', '#ff7f00', '#cab2d6','#6a3d9a', '#e585cf', '#ad009d'])
    #sns.palplot(Paired)
    Infographics = sns.color_palette(['#e8615d', '#f49436', '#2d9de5', '#3bbdbd', '#634792'])
    #sns.palplot(Infographics)
    
    def pca(matrix, labels=None, n_components=2):
        sklearn_pca = PCA(n_components=n_components)
        sklearn_pca.fit(matrix)
        transform = sklearn_pca.transform(matrix)
        df = pd.DataFrame()
        for i in range(n_components):
            df[f'PC{i+1}'] = transform[:, i]
        if labels is not None:
            df['labels'] = labels
        return df

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

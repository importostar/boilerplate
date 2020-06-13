---
title: scatterplot (1)
date: 2020-05-07
---
Example Python program scatterplot (1).py

## Modules

* import mpld3
* import numpy as np
* import pandas
* import matplotlib
* import matplotlib.cm as cm
* import matplotlib.lines as mlines
* import matplotlib.pyplot as plt

## Methods

* def scatterplot(data=None, x=None, y=None, cat=None, sizecat=None, labels=None,

## Code

Python example

    """Interactive scatter plot using MPLD3 with API inspired by seaborn."""
    import mpld3
    import numpy as np
    import pandas
    import matplotlib
    import matplotlib.cm as cm
    import matplotlib.lines as mlines
    import matplotlib.pyplot as plt
    
    
    def scatterplot(data=None, x=None, y=None, cat=None, sizecat=None, labels=None,
                    cmap='Set1', alpha=0.5, figsize=(12, 10), markersize=100,
                    graybg=False):
        """Create scatter plot with labels as tooltips shown on mouse-over.
    
        Input is a DataFrame, the other parameters are column names and tweaks.
        :param x, y: column names which hold the x, y coordinates, or array-likes.
        :param cat: (column name for) category labels of data points; each category
            is drawn in a different color and appears in the legend.
        :param sizecat: numeric data to display by adjusting the size of data
            points.
        :param labels: labels for individual data points shown as tooltips.
        :param cmap: name of a matplotlib colormap.
        :param alpha: level of transparency of data points.
        :param figsize: size of plot (width, height).
        :param markersize: if sizecat is not given, the default size of data
            points.
        :param graybg: use gray instead of white background.
        :returns: a Figure.
    
        Usage:
        >>> scatterplot(df)  # use first two columns as x, y coordinates
        >>> scatterplot(x=[...], y=[...])  # plot given array-likes
        >>> scatterplot(df, x='col1', y='col1', ...)  # specify column names to use
        >>> mpld3.display()  # display figure in e.g., notebook
        """
        fig, ax = plt.subplots(
            subplot_kw=dict(axisbg='#EEEEEE') if graybg else None,
            figsize=figsize)
        if data is None:
            data = pandas.DataFrame({'x': x, 'y': y}, index=labels)
            x, y = 'x', 'y'
        elif x is None and y is None:
            x, y = data.columns[~data.columns.isin([cat, sizecat, labels])][:2]
        if isinstance(cat, str):
            cat = data[cat]
        if isinstance(sizecat, str):
            sizecat = data[sizecat]
        # labels for categories:
        if cat is None:
            cat = np.ones(len(data))
            categorylabels = [1]
        else:
            categorylabels = cat.unique()
        # labels for data points:
        if labels is None:
            labels = data.index
        elif isinstance(labels, str):
            labels = data[labels]
        # colors for categories:
        norm = matplotlib.colors.Normalize(vmin=0, vmax=len(categorylabels))
        mappable = cm.ScalarMappable(norm, cmap)
        mappable.set_array(range(len(categorylabels)))
        colors = mappable.to_rgba(range(len(categorylabels)))
    
        for a, c in zip(categorylabels, colors):
            scatter = ax.scatter(
                    data[cat == a][x],
                    data[cat == a][y],
                    color=c,
                    s=markersize if sizecat is None
                        else (5 * sizecat[cat == a] ** 2),
                    alpha=alpha,
                    label=a)
            tooltip = mpld3.plugins.PointLabelTooltip(
                    scatter,
                    labels=[labels[n] for n in (cat == a).nonzero()[0]])
            mpld3.plugins.connect(fig, tooltip)
        # plt.title(cat)
        ax.set_xlabel(x)
        ax.set_ylabel(y)
        # work around limitation of mpld3 wrt markers in legends
        ax.legend(loc='best', framealpha=0, numpoints=1, handles=[
                mlines.Line2D(range(1), range(1), color="white", marker='o',
                    markerfacecolor=c, label=a)
                for a, c in zip(categorylabels, colors)])
        return fig
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

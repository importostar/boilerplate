---
title: matplotlib_trajectories
date: 2020-05-07
---
Example Python program matplotlib_trajectories.py

## Modules

* import matplotlib as mpl
* import matplotlib.pyplot as plt
* import numpy as np

## Methods

* def plot_trajectories(lst, ax=None, colors=None, cmap=None, alpha=None, ):

## Code

Python example

    import matplotlib as mpl
    import matplotlib.pyplot as plt
    import numpy as np
    
    
    
    def plot_trajectories(lst, ax=None, colors=None, cmap=None, alpha=None, ):
        """Plot trajectories via matplotlib's line segments.
        
        Parameters
        ----------
        lst: sequence of sequence containing points
            For example, a list of numpy arrays, where each array contains the points along
            a trajectory, e.g., [(x0, y0), (x1, y1), ..., (xn, yn)].
        ax: matplotlib axis, optional 
            The axis on which to plot. If not provided, an axis is created.
        colors: sequence of sequence of floats, optional
            A list of the same "shape" as `lst`, containing the colors that should be associated
            with each point along the trajectory
        cmap: matplotlib colormap, optional
            Colormap to use for the trajectories.
        alpha:
            Transparency value for the line segments.
            
        """
        if ax is None:
            fig, ax = plt.subplots()
            
        for ix, pts in enumerate(lst):
            line = pts.reshape(-1, 1, 2)
            segments = np.concatenate([line[:-1], line[1:]], axis=1)
            
            # create line segments and apply options
            lc = mpl.collections.LineCollection(segments, cmap=cmap)
            if alpha is not None:
                lc.set_alpha(alpha)
            if colors is not None:
                lc.set_array(colors[ix])
    
            # plot the segment
            ax.add_collection(lc)
        return ax
    
    
    # For example, we plot some curves that are slightly offset from one another
    """
    #xvals = [np.sin(np.linspace(0, 4*np.pi)) for i in range(10)]
    >>> xvals = [np.linspace(-1.5, 1.5) for i in range(10)]
    >>> yvals = [i*0.1 + np.linspace(0,1)*np.cos(np.linspace(0, 4*np.pi)) for i in range(10)]
    >>> tlst = np.array([[(x, y) for x, y in zip(i, j)] for i, j in zip(xvals, yvals)])
    >>> np.shape(tlst)
    (10, 50, 2)
    
    # Plot the trajectories
    >>> fig, ax = plt.subplots()
    >>> plot_trajectories(tlst, ax=ax)
    
    # Adjust limits
    >>> ax.set_xlim([-2,2])
    >>> ax.set_ylim([-2, 2])
    """

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

---
title: matrix_plotting
date: 2020-05-07
---
Example Python program matrix_plotting.py

## Modules

* import numbers
* import collections
* import matplotlib.pyplot as plt
* import numpy as np
* from nilearn._utils.compat import _basestring

## Classes

* class ConnectomeVisualizer(object):

## Methods

* def _data_check(data, labels):
* def __init__(self, matrix, axes=None, figure=None, figsize=(8, 8),
* def _init_figure(self, axes, figure, figsize, facecolor):
* def _data_show(self, matrix, labels, view_type=''):
* def _data_ranges(self, data, vmax, vmin):
* def _show_colorbar(self):
* def plot_matrix_square(matrix, labels=None, figure=None, axes=None,

## Code

Python example

    """ Functions to plot connectivity matrices, either as a square or circular.
    """
    
    import numbers
    import collections
    import matplotlib.pyplot as plt
    import numpy as np
    
    from nilearn._utils.compat import _basestring
    
    
    def _data_check(data, labels):
        """To check consitencies in length
        """
    
    
    class ConnectomeVisualizer(object):
        """A class which creates an instance of axes object with adjusting
        labels, vmin, vmax.
        """
        def __init__(self, matrix, axes=None, figure=None, figsize=(8, 8),
                     facecolor='w', vmin=None, vmax=None, symmetric=True,
                     cmap='RdBu_r', colorbar=False, interpolation='nearest'):
            """Create axes for plotting connectome matrices
    
            Parameters
            ----------
            axes : matplotlib axes object, optional
                The axes on which matrices will be plotted.
            """
            fig, ax = self._init_figure(axes=axes, figure=figure, figsize=figsize,
                                        facecolor=facecolor)
            self.fig = fig
            self.ax = ax
            self.symmetric = symmetric
    
            vmin, vmax = self._data_ranges(matrix, vmin=vmin, vmax=vmax)
            self.vmin = vmin
            self.vmax = vmax
    
            if isinstance(cmap, _basestring):
                self.cmap = plt.cm.get_cmap(cmap)
    
            self.colorbar = colorbar
            self.interpolation = interpolation
    
        def _init_figure(self, axes, figure, figsize, facecolor):
            """Initialize the figure
            """
            if figure is not None and not isinstance(figure, plt.Figure):
                raise ValueError("The given 'figure' must be matplotlib instance "
                                 "like matplotlib.pyplot.Figure. You provided {0}"
                                 .format(figure))
    
            if figsize is not None and not isinstance(figsize, tuple):
                raise ValueError("'figsize' tuple is expected (width, height). "
                                 "You provided {0}".format(figsize))
    
            if axes is not None and not isinstance(axes, plt.Axes):
                raise ValueError("The given 'axes' must be matplotlib instance "
                                 "like matplotlib.pyplot.Axes. You provided {0}"
                                 .format(axes))
            if axes is None:
                axes = [0., 0., 1., 1.]
    
            if figure is None:
                figure = plt.figure(figsize=figsize, facecolor=facecolor)
    
            if not isinstance(axes, plt.Axes) and isinstance(figure, plt.Figure):
                axes = figure.add_axes(axes)
                axes = figure.axes[0]
    
            if isinstance(axes, plt.Axes) and isinstance(figure, plt.Figure):
                if axes.figure != figure:
                    axes = figure.add_axes(axes)
                    axes = figure.axes[0]
    
            axes.axis('off')
            return figure, axes
    
        def _data_show(self, matrix, labels, view_type=''):
            """Visualize a matrix
            """
            ax = self.ax
            ax.imshow(matrix, interpolation="nearest", vmin=self.vmin,
                      vmax=self.vmax, cmap=self.cmap)
    
            if self.colorbar:
                self._show_colorbar()
    
        def _data_ranges(self, data, vmax, vmin):
            """
            """
            if vmin is None:
                vmin = np.nanmin(data)
    
            if vmax is None:
                vmax = np.nanmax(data)
    
            if self.symmetric:
                vmax = max(abs(vmin), abs(vmax))
                vmin = -vmax
    
            return vmin, vmax
    
        def _show_colorbar(self):
            """
            """
    
    
    def plot_matrix_square(matrix, labels=None, figure=None, axes=None,
                           facecolor=None, cmap='RdBu_r', **kwargs):
        """Plot matrix type data using matplotlib imshow.
    
        Parameters
        ----------
        matrix : numpy.ndarray (n, n)
            Connectivity matrix. 2D array-like data to visualize.
    
        labels : numpy array like or list (n,)
            Labels attached to each node in the matrix. Expected number
            of labels should match to shape of matrix (n). By default,
            no labels will be displayed.
    
        figure : instance of matplotlib.pyplot.Figure, optional
            Matplotlib figure to use. If an instance of matplotlib figure
            is given, the same will be used for plotting. By default, figure
            of size (8, 8) will be created.
    
        figsize : int, tuple (width, height), optional
            Size of the figure. If given, this figure size will replace the
            default figsize (8, 8).
    
        facecolor : str, optional
            The color for the background in figure. By default, color is white 'w'.
    
        interpolation : str {'nearest'}
        """
    
        if matrix is None:
            raise ValueError("Matrix should not be provided as None")
    
        if isinstance(matrix, _basestring) or isinstance(matrix, numbers.Number):
            raise ValueError("The 'matrix' should be of 2D numpy array like (n, n)."
                             " You provided {0}".format(matrix))
    
        if not isinstance(matrix, np.ndarray):
            matrix = np.asarray(matrix)
    
        matrix = np.nan_to_num(matrix)
    
        matrix_shape = matrix.shape
    
        if len(matrix_shape) != 2 or (matrix_shape[0] != matrix_shape[1]):
            raise ValueError("Data matrix should be 2D (n, n), got an array of shape"
                             " {0}".format(matrix_shape))
    
        if labels is not None:
            if isinstance(labels, _basestring) or isinstance(labels, numbers.Number):
                raise ValueError("The given 'labels' must be of 1D numpy array like"
                                 " or list. You provided {0}".format(labels))
            else:
                if (isinstance(labels, collections.Iterable) or
                        not isinstance(labels, np.ndarray)):
                    labels = np.asarray(labels)
    
        if labels is not None and len(labels.shape) != 1:
            raise ValueError("Number of labels given must be shape of (n,). You"
                             " provided {0}".format(labels.shape))
    
        if matrix_shape[0] != labels.shape[0]:
            raise ValueError("Shape mismatch between 'matrix' {0} and 'labels' {1}."
                             .format(matrix_shape, labels.shape))
    
        return matrix

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

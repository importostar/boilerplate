---
title: iplot
date: 2020-05-07
---
Example Python program iplot.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import numpy as np
* from matplotlib import pyplot as plt
* from sherpa.astro import ui
* from sherpa.astro.data import DataIMG

## Methods

* def _get_extent(d):
* def _plot_pixvals(pixvals, extent, scale=None):
* def _old_plot_idata(id=None, overplot=False, scale=None):
* def _old_plot_imodel(id=None, overplot=False, scale=None):
* def _plot_image(accessor, id=None, overplot=False, scale=None):
* def plot_idata(id=None, overplot=False, scale=None):
* def plot_imodel(id=None, overplot=False, scale=None):
* def plot_isource(id=None, overplot=False, scale=None):
* def plot_iresid(id=None, overplot=False, scale=None):

## Code

Python example

    """
    Provide basic plot commands for Sherpa image; the idea is to allow
    data to be displayed using the plot backend (matplotlib or chips)
    rather than ds9. This is useful for scripts or notebook.
    
    At present only matplotlib is used (it is not properly abstracted
    to use a backend).
    
    I think that we could have 'plot_data()' - and related - do this, but
    for now we have
    
        plot_idata()
    
    """
    
    import numpy as np
    
    from matplotlib import pyplot as plt
    
    from sherpa.astro import ui
    from sherpa.astro.data import DataIMG
    
    
    def _get_extent(d):
        """Return the extent array for a dataset.
    
        Parameters
        ----------
        d : DataIMG instance
    
        Returns
        -------
        extent : 4-element tuple
            This is the extent values for the plt.imshow command, giving
            the left, right, bottom, and top coordinates of the corner
            pixels (the opposoing corners of these pixels).
    
        Notes
        -----
        Only logical and physical coordinate systems are supported;
        world is replaced by physical and any other by logical.
        """
    
        # The imshow extent argument takes (left, right, bottom, top)
        # values, which give the coordinates of the corners of the lower-left
        # and top-right pixels. If there has been no filtering then could
        # just use the min and max values of the .x0 and .x1 attributes
        # (but would still have to shift them to convert from pixel center
        # to pixel edge).
        #
        # Fall back to the logical system for unknown coordinates.
        #
        ny, nx = d.shape
        x0 = [0.5, 0.5]
        x1 = [nx + 0.5, ny + 0.5]
    
        if d.coord in ['physical', 'world']:
            if d.coord == 'world':
                print("WARNING: using physical coordinates for display")
    
            x0 = d.sky.apply(*x0)
            x1 = d.sky.apply(*x1)
    
        elif d.coord != 'logical':
            print("WARNING: unknown coordinate system {}".format(d.coord))
    
        return (x0[0], x1[0], x0[1], x1[1])
    
    
    def _plot_pixvals(pixvals, extent, scale=None):
        """Display the pixel values.
    
        Parameters
        ----------
        pixvals : 2D NumPy array
        extent : 4-element sequence
            The extent argument for imshow
        scale : None or function
            The function to scale the image values.
    
        """
    
        if scale is not None:
            ovals = np.seterr(all='ignore')
            try:
                pixvals = scale(pixvals)
            finally:
                np.seterr(**ovals)
    
        plt.imshow(pixvals, origin='lower', extent=extent)
    
    
    def _old_plot_idata(id=None, overplot=False, scale=None):
        """Display the image as a plot.
    
        The scale argument is a quick hack. There may be better ways of
        doing it - e.g. matplotlib.colors.Normalize.
    
        Parameters
        ----------
        id : int or str or None, optional
           The data set that provides the data. If not given then the
           default identifier is used, as returned by `get_default_id`.
        overplot : bool, optional
           If ``True`` then add the data to an exsiting plot, otherwise
           create a new plot. The default is ``False``.
        scale : function or None, optional
           If not None, then the pixel values are sent to this routine
           before display. Suggested values are np.log10 or np.sqrt.
    
    
        See Also
        --------
        plot_imodel
    
        Notes
        -----
        At present it is restricted to DataIMG datasets and there is no
        support for the world coordinate system (it drops back to physical).
    
        Examples
        --------
    
        Plot up the image from the default data set:
    
        >>> plot_idata()
    
        Plot the image from the 'bgimg' data set:
    
        >>> plot_idata('bgimg')
    
        Use a logarithmic scale for the image, adding a colorbar and
        clipping the display to 10^-6 to 10^-3:
    
        >>> plot_idata(scale=np.log10)
        >>> plt.colorbar()
        >>> plt.clim(-6, -3)
    
        """
    
        if id is None:
            sid = ui.get_default_id()
        else:
            sid = id
    
        d = ui.get_data(id)
        if not isinstance(d, DataIMG):
            raise TypeError("Requires a DataIMG dataset")
    
        # How best to handle overplot?
        if not overplot:
            plt.clf()
    
        # This is filtered, but is full size.
        #
        # How can we determine the logical range of the pixels of interest?
        #
        idata = d.get_img()
    
        extent = _get_extent(d)
        _plot_pixvals(idata, extent, scale)
    
    
    def _old_plot_imodel(id=None, overplot=False, scale=None):
        """Display the model as a plot.
    
        .. warning::
    
           This is *very* experimental. It is almost-certainly not going
           to work for PSF-convolved models.
    
        The scale argument is a quick hack. There may be better ways of
        doing it - e.g. matplotlib.colors.Normalize.
    
        Parameters
        ----------
        id : int or str or None, optional
           The data set that provides the model. If not given then the
           default identifier is used, as returned by `get_default_id`.
        overplot : bool, optional
           If ``True`` then add the data to an exsiting plot, otherwise
           create a new plot. The default is ``False``.
        scale : function or None, optional
           If not None, then the pixel values are sent to this routine
           before display. Suggested values are np.log10 or np.sqrt.
    
    
        See Also
        --------
        plot_idata
    
        Notes
        -----
        At present it is restricted to DataIMG datasets and there is no
        support for the world coordinate system (it drops back to physical).
    
        Examples
        --------
    
        Plot up the model from the default data set:
    
        >>> plot_imodel()
    
        Plot the model from the 'bgimg' data set:
    
        >>> plot_imodel('bgimg')
    
        """
    
        if id is None:
            sid = ui.get_default_id()
        else:
            sid = id
    
        d = ui.get_data(id)
        if not isinstance(d, DataIMG):
            raise TypeError("Requires a DataIMG dataset")
    
        # mdl = ui.get_source(id)
        mdl = ui.get_model(id)
    
        # How best to handle overplot?
        if not overplot:
            plt.clf()
    
        # This is filtered, but is full size.
        #
        # How can we determine the logical range of the pixels of interest?
        #
        _, mdata = d.get_img(mdl)
    
        extent = _get_extent(d)
        _plot_pixvals(mdata, extent, scale)
    
    
    # Try and piggy back on the image_xxx functionality.
    #
    def _plot_image(accessor, id=None, overplot=False, scale=None):
        """Display the image as a plot.
    
        The scale argument is a quick hack. There may be better ways of
        doing it - e.g. matplotlib.colors.Normalize.
    
        Parameters
        ----------
        accessor : function
           Returns a Model instance which has had its prepare method called.
        id : int or str or None, optional
           The data set that provides the data. If not given then the
           default identifier is used, as returned by `get_default_id`.
        overplot : bool, optional
           If ``True`` then add the data to an exsiting plot, otherwise
           create a new plot. The default is ``False``.
        scale : function or None, optional
           If not None, then the pixel values are sent to this routine
           before display. Suggested values are np.log10 or np.sqrt.
    
    
        Notes
        -----
        At present it is restricted to DataIMG datasets and there is no
        support for the world coordinate system (it drops back to physical).
    
        """
    
        if id is None:
            sid = ui.get_default_id()
        else:
            sid = id
    
        img = accessor(id)
    
        # How best to handle overplot?
        if not overplot:
            plt.clf()
    
        # There is no easy way - that I know of - to get the filtered region
        # (i.e. the bounding box of the region).
        #
        extent = _get_extent(ui.get_data(id))
        _plot_pixvals(img.y, extent, scale)
    
    
    def plot_idata(id=None, overplot=False, scale=None):
        """Display the image as a plot.
    
        The scale argument is a quick hack. There may be better ways of
        doing it - e.g. matplotlib.colors.Normalize.
    
        Parameters
        ----------
        id : int or str or None, optional
           The data set that provides the data. If not given then the
           default identifier is used, as returned by `get_default_id`.
        overplot : bool, optional
           If ``True`` then add the data to an exsiting plot, otherwise
           create a new plot. The default is ``False``.
        scale : function or None, optional
           If not None, then the pixel values are sent to this routine
           before display. Suggested values are np.log10 or np.sqrt.
    
    
        See Also
        --------
        plot_imodel, plot_iresid, plot_isource
    
        Notes
        -----
        At present it is restricted to DataIMG datasets and there is no
        support for the world coordinate system (it drops back to physical).
    
        Examples
        --------
    
        Plot up the image from the default data set:
    
        >>> plot_idata()
    
        Plot the image from the 'bgimg' data set:
    
        >>> plot_idata('bgimg')
    
        Use a logarithmic scale for the image, adding a colorbar and
        clipping the display to 10^-6 to 10^-3:
    
        >>> plot_idata(scale=np.log10)
        >>> plt.colorbar()
        >>> plt.clim(-6, -3)
    
        """
    
        _plot_image(ui.get_data_image, id=id, scale=scale, overplot=overplot)
    
    
    def plot_imodel(id=None, overplot=False, scale=None):
        """Display the model as a plot.
    
        The scale argument is a quick hack. There may be better ways of
        doing it - e.g. matplotlib.colors.Normalize.
    
        Parameters
        ----------
        id : int or str or None, optional
           The data set that provides the model. If not given then the
           default identifier is used, as returned by `get_default_id`.
        overplot : bool, optional
           If ``True`` then add the data to an exsiting plot, otherwise
           create a new plot. The default is ``False``.
        scale : function or None, optional
           If not None, then the pixel values are sent to this routine
           before display. Suggested values are np.log10 or np.sqrt.
    
    
        See Also
        --------
        plot_idata, plot_iresid, plot_isource
    
        Notes
        -----
        At present it is restricted to DataIMG datasets and there is no
        support for the world coordinate system (it drops back to physical).
    
        Examples
        --------
    
        Plot up the model from the default data set:
    
        >>> plot_imodel()
    
        Plot the model from the 'bgimg' data set:
    
        >>> plot_imodel('bgimg')
    
        """
    
        _plot_image(ui.get_model_image, id=id, scale=scale, overplot=overplot)
    
    
    def plot_isource(id=None, overplot=False, scale=None):
        """Display the source as a plot.
    
        The scale argument is a quick hack. There may be better ways of
        doing it - e.g. matplotlib.colors.Normalize.
    
        Parameters
        ----------
        id : int or str or None, optional
           The data set that provides the model. If not given then the
           default identifier is used, as returned by `get_default_id`.
        overplot : bool, optional
           If ``True`` then add the data to an exsiting plot, otherwise
           create a new plot. The default is ``False``.
        scale : function or None, optional
           If not None, then the pixel values are sent to this routine
           before display. Suggested values are np.log10 or np.sqrt.
    
    
        See Also
        --------
        plot_idata, plot_imodel, plot_iresid
    
        Notes
        -----
        At present it is restricted to DataIMG datasets and there is no
        support for the world coordinate system (it drops back to physical).
    
        Examples
        --------
    
        Plot up the source from the default data set:
    
        >>> plot_isource()
    
        Plot the source from the 'bgimg' data set:
    
        >>> plot_isource('bgimg')
    
        """
    
        _plot_image(ui.get_source_image, id=id, scale=scale, overplot=overplot)
    
    
    def plot_iresid(id=None, overplot=False, scale=None):
        """Display the resid image as a plot.
    
        The scale argument is a quick hack. There may be better ways of
        doing it - e.g. matplotlib.colors.Normalize.
    
        Parameters
        ----------
        id : int or str or None, optional
           The data set that provides the model. If not given then the
           default identifier is used, as returned by `get_default_id`.
        overplot : bool, optional
           If ``True`` then add the data to an exsiting plot, otherwise
           create a new plot. The default is ``False``.
        scale : function or None, optional
           If not None, then the pixel values are sent to this routine
           before display. Suggested values are np.log10 or np.sqrt.
    
    
        See Also
        --------
        plot_idata, plot_imodel, plot_isource
    
        Notes
        -----
        At present it is restricted to DataIMG datasets and there is no
        support for the world coordinate system (it drops back to physical).
    
        Examples
        --------
    
        Plot up the residual image from the default data set:
    
        >>> plot_iresid()
    
        Plot the residual image from the 'bgimg' data set:
    
        >>> plot_iresid('bgimg')
    
        """
    
        _plot_image(ui.get_resid_image, id=id, scale=scale, overplot=overplot)
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

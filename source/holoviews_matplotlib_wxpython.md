---
title: holoviews_matplotlib_wxpython
date: 2020-05-07
---
Example Python program holoviews_matplotlib_wxpython.py

## Modules

* import numpy as np
* import matplotlib
* import holoviews as hv
* import wx
* import xarray as xr
* from matplotlib.backends.backend_wxagg import FigureCanvasWxAgg as FigureCanvas
* #from matplotlib.backends.backend_wx import NavigationToolbar2Wx
* from matplotlib.figure import Figure

## Classes

* class CanvasPanel(wx.Panel):

## Methods

* def __init__(self, parent, figure=Figure()):

## Code

Python example

    """Example of embedding a holoviews Image in a small wxpython app through matplotlib
    
    Notes:
    * wxpython code based on example at https://stackoverflow.com/questions/10737459/embedding-a-matplotlib-figure-inside-a-wxpython-panel
    * @philippjfr showed me how to get matplotlib figure object
    """
    
    import numpy as np
    import matplotlib
    import holoviews as hv
    import wx
    import xarray as xr
    
    matplotlib.use('WXAgg')
    
    from matplotlib.backends.backend_wxagg import FigureCanvasWxAgg as FigureCanvas
    #from matplotlib.backends.backend_wx import NavigationToolbar2Wx
    from matplotlib.figure import Figure
    
    hv.extension('matplotlib')
    renderer = hv.renderer('matplotlib')
    
    
    class CanvasPanel(wx.Panel):
        def __init__(self, parent, figure=Figure()):
            wx.Panel.__init__(self, parent)
            self.figure = figure
            self.canvas = FigureCanvas(self, -1, self.figure)
            self.sizer = wx.BoxSizer(wx.VERTICAL)
            self.sizer.Add(self.canvas, 1, wx.LEFT | wx.TOP | wx.GROW)
            self.SetSizer(self.sizer)
            self.Fit()
    
    
    if __name__ == "__main__":
    
        # Data
        data = xr.DataArray(np.random.randint(1,6, (100, 100)), coords=[range(100), range(100)], dims=['x', 'y'], name="Random Land Use")
        hv_data = hv.Dataset(data, kdims=['x', 'y'], vdims='Land Use')
        img = hv_data.to(hv.Image, ['x', 'y'], vdims='Land Use')
        
        # Holoviews Image
        img = img.options(cmap=["red", "yellow", "green", "darkgreen", "black","blue"], fig_size=5000, invert_yaxis=True)
        
        # Matplolib figure
        mpl_figure = renderer.get_plot(img).state
    
        # wxpython app
        app = wx.App()
        fr = wx.Frame(None, title='test')
        panel = CanvasPanel(fr, mpl_figure)
        fr.Show()
        app.MainLoop()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

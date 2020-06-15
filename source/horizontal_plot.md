---
title: horizontal_plot
date: 2020-05-07
---
Example Python program horizontal_plot.py

## Modules

* from ipywidgets.widgets import HBox, VBox
* import matplotlib.pyplot as plt

## Methods

* def plot(s, orientation='horizontal'):

## Code

Python example

    from ipywidgets.widgets import HBox, VBox
    import matplotlib.pyplot as plt
    
    def plot(s, orientation='horizontal'):
        """
        Plot hyperspy signals horizontally using the %matplotlib widget interface.
        Can also plot vertically using orientation='vertical'
        """
        
        # if 1D signal, just plot normal
        if not "ipympl" in plt.matplotlib.get_backend():
            raise AttributeError(
                """Only works with the ipympl backend - 
        call `pip install ipympl` and use `%matplotlib widget` as the first line in the notebook""")
        if s.axes_manager.navigation_dimension == 0:
            s.plot()
        else: 
            plt.ioff() # this prevents a plot from being shown (i.e. does not call plt.show)
            s.plot()
            nav = s._plot.navigator_plot.figure
            sig = s._plot.signal_plot.figure
            if orientation == 'horizontal':
                nav.canvas.layout.margin = "auto 0px auto 0px"
                sig.canvas.layout.margin = "auto 0px auto 0px"
                box = HBox([nav.canvas, sig.canvas])
            else:
                nav.canvas.layout.margin = "0px auto 0px auto"
                sig.canvas.layout.margin = "0px auto 0px auto"
                box = VBox([nav.canvas, sig.canvas])
            display(box)
            plt.tight_layout()
            plt.ion()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

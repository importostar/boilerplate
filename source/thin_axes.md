---
title: thin_axes
date: 2020-05-07
---
Example Python program thin_axes.py

## Modules

* from matplotlib.axes import Axes
* from matplotlib.ticker import NullLocator
* from matplotlib.projections import register_projection
* import matplotlib.axis as maxis

## Classes

* class NoTicksXAxis(maxis.XAxis):
* class NoTicksYAxis(maxis.YAxis):
* class ThinAxes(Axes):

## Methods

* def reset_ticks(self):
* def set_clip_path(self, clippath, transform=None):
* def reset_ticks(self):
* def set_clip_path(self, clippath, transform=None):
* def _init_axis(self):
* def cla(self):
* def _gen_axes_spines(self):

## Code

Python example

    from matplotlib.axes import Axes
    from matplotlib.ticker import NullLocator
    from matplotlib.projections import register_projection
    import matplotlib.axis as maxis
    
    class NoTicksXAxis(maxis.XAxis):
        def reset_ticks(self):
            self._lastNumMajorTicks = 1
            self._lastNumMinorTicks = 1
        def set_clip_path(self, clippath, transform=None):
            pass
    
    class NoTicksYAxis(maxis.YAxis):
        def reset_ticks(self):
            self._lastNumMajorTicks = 1
            self._lastNumMinorTicks = 1
        def set_clip_path(self, clippath, transform=None):
            pass
    
    class ThinAxes(Axes):
        """Thin axes without spines and ticks to accelerate axes creation"""
    
        name = 'thin'
    
        def _init_axis(self):
            self.xaxis = NoTicksXAxis(self)
            self.yaxis = NoTicksYAxis(self)
    
        def cla(self):
            """
            Override to set up some reasonable defaults.
            """
            Axes.cla(self)
            self.xaxis.set_minor_locator(NullLocator())
            self.yaxis.set_minor_locator(NullLocator())
            self.xaxis.set_major_locator(NullLocator())
            self.yaxis.set_major_locator(NullLocator())
    
        def _gen_axes_spines(self):
            return {}
                   
    
    # Now register the projection with matplotlib so the user can select
    # it.
    register_projection(ThinAxes)

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

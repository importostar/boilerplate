---
title: datathoughts
date: 2020-05-07
---
Example Python program datathoughts.py

## Modules

* import numpy as np
* import matplotlib
* import matplotlib.lines
* from matplotlib.artist import allow_rasterization
* import matplotlib.pyplot as plt

## Classes

* class MatplotlibException(Exception):
* class InvalidDatasource(MatplotlibException, ValueError):
* class SimpleSource:
* class DFSource:
* class FuncSource1D:
* class DSLine2D(matplotlib.lines.Line2D):

## Methods

* def __init__(self, **kwargs):
* def get(self, keys, ax=None, renderer=None):
* def __init__(self, df, **kwargs):
* def get(self, keys, ax, renderer):
* def __init__(self, func):
* def get(self, keys, ax, renderer):
* def __init__(self, DS, **kwargs):
* def draw(self, renderer):

## Code

Python example

    import numpy as np
    import matplotlib
    import matplotlib.lines
    from matplotlib.artist import allow_rasterization
    import matplotlib.pyplot as plt
    
    
    class MatplotlibException(Exception):
        ...
    
    
    class InvalidDatasource(MatplotlibException, ValueError):
        ...
    
    
    class SimpleSource:
        def __init__(self, **kwargs):
            self._data = {k: np.asanyarray(v) for k, v in kwargs.items()}
            self.md = {k: {"ndim": v.ndim, "dtype": v.dtype} for k, v in self._data.items()}
    
        def get(self, keys, ax=None, renderer=None):
            return {k: self._data[k] for k in keys}
    
    
    class DFSource:
        def __init__(self, df, **kwargs):
            self._remapping = kwargs
            self._data = df
            self.md = {k: {"ndim": 1, "dtype": df[v].dtype} for k, v in kwargs.items()}
    
        def get(self, keys, ax, renderer):
            return {k: self._data[self._mapping[k]] for k in keys}
    
    
    class FuncSource1D:
        def __init__(self, func):
            self._func = func
            self.md = {"x": {"ndim": 1, "dtype": float}, "y": {"ndim": 1, "dtype": float}}
    
        def get(self, keys, ax, renderer):
            assert set(keys) == set(self.md)
            xlim = ax.get_xlim()
            bbox = ax.get_window_extent(renderer)
            xpixels = bbox.width
            x = np.linspace(*xlim, xpixels)
            return {"x": x, "y": self._func(x)}
    
    
    class DSLine2D(matplotlib.lines.Line2D):
        def __init__(self, DS, **kwargs):
            if not all(k in DS.md for k in ("x", "y")):
                raise InvalidDatasource
            self._DS = DS
            super().__init__([], [], **kwargs)
    
        @allow_rasterization
        def draw(self, renderer):
    
            data = self._DS.get({"x", "y"}, self.axes, renderer)
            super().set_data(data["x"], data["y"])
    
            return super().draw(renderer)
    
    
    plt.close("all")
    ax = plt.gca()
    DS = SimpleSource(x=np.linspace(0, 10, 100), y=np.sin(np.linspace(0, 10, 100)))
    
    DS2 = FuncSource1D(lambda x: np.cos(x) + 1)
    dsl = DSLine2D(DS, color="red")
    ax.add_artist(dsl)
    dsl2 = DSLine2D(DS2, color="blue")
    ax.add_artist(dsl2)
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

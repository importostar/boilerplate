---
title: matplotlib_cubehelix
date: 2020-05-07
---
Example Python program matplotlib_cubehelix.py

## Modules

* import bisect
* import numpy
* import matplotlib.colors
* import matplotlib.cm

## Classes

* class CubehelixColormap(matplotlib.colors.Colormap):

## Methods

* def __init__(self, name, ch_controlpoints = (
* def _interpolateCubehelix(self, x):
* def _init(self):
* def set_gamma(self, gamma):

## Code

Python example

    # a cubehelix colourmap implementation, following http://bl.ocks.org/mbostock/310c99e53880faec2434
    import bisect
    import numpy
    import matplotlib.colors
    import matplotlib.cm
    
    class CubehelixColormap(matplotlib.colors.Colormap):
        def __init__(self, name, ch_controlpoints = (
                (0.0, (+300.0, 0.5, 0.0)),
                (1.0, (-240.0, 0.5, 1.0))
            ), N=256, gamma = 1.0):
            super(CubehelixColormap, self).__init__(name, N)
            self._ch_cp_pos, self._ch_cp_val = zip(*ch_controlpoints)
            self._ch_cp_pos = map(float, self._ch_cp_pos)
            self._ch_cp_val = numpy.array(self._ch_cp_val, dtype=numpy.float)
            self._ch_cp_val[:,0] = numpy.radians(self._ch_cp_val[:,0] + 120)
            self._gamma = gamma
    
        def _interpolateCubehelix(self, x):
            i = bisect.bisect_right(self._ch_cp_pos, x)-1
            if i == -1:
                a, b, x = self._ch_cp_val[0], self._ch_cp_val[0], 0.0
            elif i == len(self._ch_cp_pos)-1:
                a, b, x = self._ch_cp_val[i], self._ch_cp_val[i], 0.0
            else:
                ax, bx = self._ch_cp_pos[i], self._ch_cp_pos[i+1]
                a, b = self._ch_cp_val[i], self._ch_cp_val[i+1]
                x = (x - ax) / (bx - ax)
    
            a_h, a_s, a_l = a
            b_h, b_s, b_l = b - a
    
            h = a_h + b_h * x
            l = (a_l + b_l * x) ** self._gamma
            a = (a_s + b_s * x) * l * (1 - l)
    
            cosh = math.cos(h)
            sinh = math.sin(h)
    
            return (
                l + a * (-0.14861 * cosh + 1.78277 * sinh),
                l + a * (-0.29227 * cosh - 0.90649 * sinh),
                l + a * (+1.97294 * cosh),
                1.0
            )
    
        def _init(self):
            lut = numpy.clip(numpy.array([ self._interpolateCubehelix(x) for x in numpy.linspace(0, 1, self.N) ]), 0.0, 1.0)
            self._lut = numpy.ones((self.N + 3, 4), numpy.float)
            self._lut[:-3] = lut
            self._isinit = True
            self._set_extremes()
    
        def set_gamma(self, gamma):
            self._gamma = gamma
            self._init()
    
    matplotlib.cm.register_cmap(cmap = CubehelixColormap('cubehelix'))
    matplotlib.cm.register_cmap(cmap = CubehelixColormap('cubehelix_rainbow', (
      (0.0, (-100, 0.75, 0.35)),
      (0.5, (  80, 1.50, 0.80)),
      (1.0, ( 260, 0.75, 0.35))
    )))

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

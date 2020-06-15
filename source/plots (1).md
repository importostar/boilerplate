---
title: plots (1)
date: 2020-05-07
---
Example Python program plots (1).py

## Modules

* import math
* import numpy as np
* import matplotlib.pyplot as plt

## Methods

* def plot_points(subplot, points, fx=lambda x: x):
* def plot_ranges(subplot, ranges, fx=lambda x: x):
* def plot_func_ranges(subplot, ranges, fx):
* def plot_range_ties(subplot, ranges, fx1, fx2):
* def constant(x=0):
* def identity(x):
* def voffset(f, offset):
* def scratch():
* def scratch_multi():
* def f(x):

## Code

Python example

    import math
    
    import numpy as np
    import matplotlib.pyplot as plt
    
    
    # Points
    def plot_points(subplot, points, fx=lambda x: x):
        xs = points
        ys = map(fx, xs)
        subplot.plot(xs, ys, 'C1X',
                     linestyle=':',
                     linewidth=0.5,
                     )
    
    
    # Ranges
    def plot_ranges(subplot, ranges, fx=lambda x: x):
        plot_func_ranges(subplot, ranges, fx)
    
    
    # Continuous
    def plot_func_ranges(subplot, ranges, fx):
        for r in ranges:
            xs = np.linspace(r[0], r[1], 1000)
            ys = map(fx, xs)
            subplot.plot(xs, ys, 'C1')
            subplot.plot([xs[0], xs[-1]], [ys[0], ys[-1]], 'C1|')
    
    
    # Vertical lines tying two ranges together
    def plot_range_ties(subplot, ranges, fx1, fx2):
        range_xs = [pt for r in ranges for pt in r]
        for x in range_xs:
            xs = [x, x]
            ys = [fx1(x), fx2(x)]
            subplot.plot(xs, ys, 'C2', linestyle=':')
    
    
    def constant(x=0):
        return lambda n: x
    
    
    def identity(x):
        return x
    
    
    def voffset(f, offset):
        return lambda x: f(x) + offset
    
    
    def scratch():
        fig = plt.figure()
        ax = fig.add_subplot(1, 1, 1)
    
        plot_points(ax, [0.1, 1, 1.5, 5.2, 7], voffset(constant(), 5))
        plot_ranges(ax, [[0, 4], [6, 8]], voffset(constant(), 4))
        plot_func_ranges(ax, [[0, 10]], voffset(math.sin, 2))
        plot_func_ranges(ax, [[0, 4], [6, 8]], voffset(math.sin, 0))
        plot_range_ties(ax, [[0, 4], [6, 8]], voffset(constant(), 4), voffset(math.sin, 0))
    
        return fig
    
    
    def scratch_multi():
        fig, (ax1, ax2, ax3, ax4) = plt.subplots(4, 1, sharex='col')
    
        # Common
        def f(x):
            n = math.sin(x) * 5
            return math.sin(n) * n
    
        # Primitives
        plot_points(ax1, [0.1, 1, 1.5, 5.2, 7], voffset(constant(), 5))
        plot_ranges(ax1, [[0, 4], [6, 8]], voffset(constant(), 4))
        plot_func_ranges(ax1, [[0, 10]], voffset(f, 2))
    
        # Metric function subsets
        plot_ranges(ax2, [[0, 4], [6, 8]], voffset(constant(), 4))
        plot_func_ranges(ax2, [[0, 10]], voffset(f, 2))
        plot_func_ranges(ax2, [[0, 4], [6, 8]], voffset(f, 0))
        plot_range_ties(ax2, [[0, 4], [6, 8]], voffset(constant(), 4), voffset(f, 0))
    
        # Point subsets
        plot_ranges(ax3, [[0, 4], [6, 8]], voffset(constant(), 1))
        plot_points(ax3, [0.1, 1, 1.5, 5.2, 7], voffset(constant(), 0))
    
        # Point combinations
        # A
        plot_ranges(ax4, [[0, 4], [5, 9]], voffset(constant(), 0))
        # B
        plot_ranges(ax4, [[0, 2], [4, 6], [8, 10]], voffset(constant(), -1))
        # ~A
        plot_ranges(ax4, [[4, 5], [9, 10]], voffset(constant(), -2))
        # ~B
        plot_ranges(ax4, [[2, 4], [6, 8]], voffset(constant(), -3))
        # A && B
        plot_ranges(ax4, [[0, 2], [5, 6], [8, 9]], voffset(constant(), -4))
        # A || B
        plot_ranges(ax4, [[0, 4], [5, 10]], voffset(constant(), -5))
    
        return fig
    
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

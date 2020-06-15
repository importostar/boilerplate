---
title: utilities
date: 2020-05-07
---
Example Python program utilities.py

## Modules

* from __future__ import division
* import copy
* import sympy
* import matplotlib
* import matplotlib.pyplot as pyplot

## Classes

* class Plot(object):

## Methods

* def setup():
* def force_sympy(func):
* def wrapper(*args, **kwargs):
* def cis(theta):
* def find_distance(a, b):
* def de_moivre(n, radius, theta):
* def tup(number):
* def __init__(self, xrange, yrange, xinterval, yinterval, figsize=(8,8)):
* def add_points(self, numbers, color=None, **kwargs):
* def add_circle(self, radius, origin=(0, 0), color='lightgreen', 
* def add_line(self, a, b, color='red', **kwargs):
* def add_annotation(self, string, coords, offset=(0, 0), **kwargs):
* def copy(self):
* def center_origin(axis):
* def add_axis_labels(axis, xrange, yrange, xinterval, yinterval):
* def fix(string):
* def x_format_func(x, pos):
* def y_format_func(y, pos):
* def render(plot):
* def save(figure, name):
* def block():

## Code

Python example

    #!/usr/bin/env python
    # -*- coding: utf-8 -*-
    
    from __future__ import division
    
    import copy
    
    # Mathematical libraries
    import sympy
    import matplotlib
    import matplotlib.pyplot as pyplot
    
    S = sympy.sympify
    R = sympy.Rational
    
    
    # Functions to help set up the mathematical libraries
    def setup():
        sympy.init_printing(use_unicode=False, wrap_line=False, no_global=True)
        matplotlib.rc('text', usetex=True)
    
    def force_sympy(func):
        '''An annotation which forces all input to be converted into Sympy objects,
        which gives the mathematical calculations greater precision.'''
        def wrapper(*args, **kwargs):
            new_args = []
            new_kwargs = {}
            for arg in args:
                if isinstance(arg, (int, long, float, complex)):
                    new_args.append(R(arg))
                else:
                    new_args.append(arg)
            for key, item in kwargs.items():
                if isinstance(item, (int, long, float, complex)):
                    new_kwargs[key] = R(item)
                else:
                    new_kwargs[key] = item
            return func(*new_args, **new_kwargs)
        wrapper.__name__ = func.__name__
        wrapper.__doc__ = func.__doc__
        return wrapper
    
    @force_sympy
    def cis(theta):
        # Note that in Python, complex numbers are represented using the 'j' 
        # character instead of the 'i' character, for whatever reason.
        return sympy.cos(theta) + sympy.sin(theta)*1j
        
    @force_sympy
    def find_distance(a, b):
        '''Finds the distance between two points'''
        ax, ay = sympy.re(a), sympy.im(a)
        bx, by = sympy.re(b), sympy.im(b)
        return sympy.sqrt((ax - bx)**R(2) + (ay - by)**R(2))
        
    @force_sympy
    def de_moivre(n, radius, theta):
        '''Returns all the roots using de Moivre's theorem'''
        magnitude = radius**(1 / n)
        return [magnitude * cis((theta + k * 2 * sympy.pi) / n) for k in range(n)]
        
    @force_sympy
    def tup(number):
        '''Converts a complex number into a Cartesian coordinate.'''
        return (sympy.re(number), sympy.im(number))
        
    
    
    class Plot(object):
        '''An object representing a graph.'''
        def __init__(self, xrange, yrange, xinterval, yinterval, figsize=(8,8)):
            self.xrange = xrange
            self.yrange = yrange
            self.xinterval = xinterval
            self.yinterval = yinterval
            self.figsize = figsize
            self.points = []
            self.circles = []
            self.lines = []
            self.annotations = []
            
        def add_points(self, numbers, color=None, **kwargs):
            '''Adds a series of complex numbers in a list to the plot.'''
            x = [sympy.re(num) for num in numbers]
            y = [sympy.im(num) for num in numbers]
            
            args = (x, y)
            kwargs['color'] = color
            
            self.points.append((args, kwargs))
            
        def add_circle(self, radius, origin=(0, 0), color='lightgreen', 
                       facecolor='none', **kwargs):
            args = (origin,)
            kwargs['radius'] = radius
            kwargs['edgecolor'] = color
            kwargs['facecolor'] = facecolor
            self.circles.append((args, kwargs))
            
        def add_line(self, a, b, color='red', **kwargs):
            x1, y1 = tup(a)
            x2, y2 = tup(b)
            args = ((x1, x2), (y1, y2))
            kwargs['color'] = color
            kwargs['zorder'] = 3
            self.lines.append((args, kwargs))
            
        def add_annotation(self, string, coords, offset=(0, 0), **kwargs):
            '''Adds text.'''
            args = (string,)
            kwargs['xy'] = coords
            kwargs['xycoords'] = 'data'
            kwargs['xytext'] = offset
            kwargs['textcoords'] = 'offset points'
            kwargs['zorder'] = 4
            self.annotations.append((args, kwargs))
            
        def copy(self):
            '''Returns a copy of this object.'''
            return copy.deepcopy(self)
            
            
    def center_origin(axis):
        '''Given a matplotlib axis, centers them in the middle of the image.'''
        axis.spines['right'].set_color('none')
        axis.spines['top'].set_color('none')
        axis.xaxis.set_ticks_position('bottom')
        axis.spines['bottom'].set_position(('data',0))
        axis.yaxis.set_ticks_position('left')
        axis.spines['left'].set_position(('data',0))
        
    def add_axis_labels(axis, xrange, yrange, xinterval, yinterval):
        '''Correctly formats the tick labels based on the script object'''
        def fix(string):
            if string.startswith('.'):
                string = '0' + string
            if string.endswith('.'):
                string = string + '0'
            return string
            
        def x_format_func(x, pos):
            return '$' + fix(('%F' % x).strip('0')) + '$'
        def y_format_func(y, pos):
            return '$' + fix(('%F' % y).strip('0')) + 'i$' if y != 0 else ''
            
        x_formatter = matplotlib.ticker.FuncFormatter(x_format_func)
        y_formatter = matplotlib.ticker.FuncFormatter(y_format_func)
        
        x_locator = matplotlib.ticker.MultipleLocator(xinterval)
        y_locator = matplotlib.ticker.MultipleLocator(yinterval)
        
        axis.xaxis.set_major_formatter(x_formatter)
        axis.xaxis.set_major_locator(x_locator)
        axis.yaxis.set_major_formatter(y_formatter)
        axis.yaxis.set_major_locator(y_locator)
        
        axis.set_xlim(*xrange)
        axis.set_ylim(*yrange)
        
    def render(plot):
        '''Converts a plot into a matplotlib figure which can then be turned
        into a png'''
        figure = pyplot.figure(figsize=plot.figsize)
        axis = figure.add_subplot(1, 1, 1)
        
        for args, kwargs in plot.points:
            axis.scatter(*args, **kwargs)
        for args, kwargs in plot.circles:
            axis.add_patch(pyplot.Circle(*args, **kwargs))
        for args, kwargs in plot.lines:
            axis.add_line(pyplot.Line2D(*args, **kwargs))
        for args, kwargs in plot.annotations:
            axis.annotate(*args, **kwargs)
            
        
        center_origin(axis)
        add_axis_labels(axis, plot.xrange, plot.yrange, 
            plot.xinterval, plot.yinterval)
        
        return figure
        
    def save(figure, name):
        '''Saves a rendered plot to a folder.'''
        path = ''.join([
            './images/',
            name,
            '.png'])
        figure.savefig(path, bbox_inches='tight')
        
    
    def block():
        '''Halts execution until user input.'''
        raw_input('Continue? >>>')
        
        
        

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

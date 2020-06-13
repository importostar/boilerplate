---
title: basic_numpy
date: 2020-05-07
---
Example Python program basic_numpy.py

## Modules

* # from pylab import *

## Code

Python example

    # If you haven't started ipython with --pylab, then do this:
    # from pylab import *
    
    # Constructing Arrays
    x = array([0,2,3,4]) # Matlab: a = [0,2,3,4];
    
    # Basic plotting
    x = arange(11)
    a = 2 * pi/10
    y = sin(a*x)
    plot(x, y)
    # If you're not on --pylab inline, do this to show the plot in a new window:
    # show()
    
    # Matlab: X = [0, 1, 2, 3 ; 10, 11, 12, 13 ; 20, 21, 22, 23]
    X = array([[0, 1, 2, 3], [10,11,12,13], [20,21,22,23]])
    print X
    
    # Array Slicing
    X[1, 2] # Row, Column
    
    # Caveat: Pass-by-Reference!
    b = X[:,2]
    print b
    b[1] = 99
    print X
    
    # Work-Around: copy first.
    Y = X.copy()
    Y[1,2] = 42
    print Y
    print X
    
    # Other ways of crating arrays:
    print zeros(5)
    print ones((2,4))
    print identity(3)
    
    # Gotchas:
    a = array(1,2,3,4)
    
    # Logical indexing:
    x = rand(100)
    x[x < .5] = 0
    scatter(range(100), x)
    
    # Polar plots
    r = rand(200)
    phi = rand(200) * 2 * pi
    polar(phi, r, 'ro')
    
    # Hexbins FTW!
    num_data = 5000.0
    x = arange(num_data) / num_data + .2
    y = x * random.normal(x, 10)
    scatter(x, y)
    hexbin(x, y, gridsize=30)

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

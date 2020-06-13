---
title: anime
date: 2020-05-07
---
Example Python program anime.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import time
* import numpy
* import matplotlib
* import matplotlib.pyplot

## Methods

* def create_dataset():
* def time_check():
* def key_press(event):
* def refresh1(fig, ax, lines):
* def refresh2(fig, ax, lines):

## Code

Python example

    # for python 3.5
    
    import time
    import numpy
    import matplotlib
    matplotlib.use('TkAgg')
    import matplotlib.pyplot
    
    step = 0.2
    start = 0
    num = 101
    
    t0 = time.time()
    
    fig = matplotlib.pyplot.figure()
    ax = fig.add_subplot(111)
    lines = ax.plot(numpy.arange(num), numpy.zeros(num))
    
    
    def create_dataset():
        global start
        global step
        global num
    
        x = numpy.linspace(start, start + 3*numpy.pi, num)
        y = numpy.sin(x)
        start += step
        
        return x, y
    
    def time_check():
        global t0
        
        t1 = time.time()
        dt = t1 - t0
        t0 = t1
        
        return dt
    
    def key_press(event):
        key = event.key
        dt = time_check()
        
        print('key: {}, dt={:.3f}'.format(key, dt))
        
        if key in [' ', 'backspace', 'right', 'left', 'up', 'down']:
            refresh(fig, ax, lines)
            pass
            
        return
    
    def refresh1(fig, ax, lines):
        x, y = create_dataset()
        ax.cla()
        ax.plot(x, y)
        ax.set_xlim(x.min(), x.max())
        ax.set_ylim(y.min(), y.max())
        fig.canvas.draw()
        return
    
    def refresh2(fig, ax, lines):
        x, y = create_dataset()
        lines[0].set_data(x, y)
        ax.set_xlim(x.min(), x.max())
        ax.set_ylim(y.min(), y.max())
        fig.canvas.draw()
        return
    
    refresh = refresh1
    #refresh = refresh2
    
    
    fig.canvas.mpl_connect('key_press_event', key_press)
    
    matplotlib.pyplot.show()
    
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

---
title: interactive_panicky
date: 2020-05-07
---
Example Python program interactive_panicky.py

## Modules

* import matplotlib
* from pylab import *
* import pycxsimulator

## Methods

* def interactive_p(val=p):
* def initialize():
* def observe():
* def update():

## Code

Python example

    import matplotlib
    matplotlib.use('TkAgg')
    from pylab import *
    
    n = 100 # size of space: n x n
    p = 0.1 # probability of initially panicky individuals
    
    def interactive_p(val=p):
        global config, nextconfig, p 
        p = float(val)
        return val 
    
    def initialize():
        global config, nextconfig, p
        config = zeros([n, n])
        for x in range(n):
            for y in range(n):
                config[x, y] = 1 if random() < p else 0
        nextconfig = zeros([n, n])
        
    def observe():
        global config, nextconfig, p
        cla()
        imshow(config, vmin = 0, vmax = 1, cmap = cm.binary)
    
    def update():
        global config, nextconfig, p
        for x in range(n):
            for y in range(n):
                count = 0
                for dx in [-1, 0, 1]:
                    for dy in [-1, 0, 1]:
                        count += config[(x + dx) % n, (y + dy) % n]
                nextconfig[x, y] = 1 if count >= 4 else 0
        config, nextconfig = nextconfig, config
    
    import pycxsimulator
    pycxsimulator.GUI(parameterSetters=[interactive_p]).start(func=[initialize, observe, update])

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

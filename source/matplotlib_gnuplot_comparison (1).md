---
title: matplotlib_gnuplot_comparison (1)
date: 2020-05-07
---
Example Python program matplotlib_gnuplot_comparison (1).py

## Modules

* from timeit import default_timer as timer
* import matplotlib.pyplot as plt
* import Gnuplot, Gnuplot.funcutils
* import numpy as np
* import sys
* import os

## Methods

* def mPlotAndSave(x, y):
* def gPlotAndSave(data, g):
* def cleanup():

## Code

Python example

    # -*- coding: utf-8 -*-
    
    from timeit import default_timer as timer
    import matplotlib.pyplot as plt
    import Gnuplot, Gnuplot.funcutils
    import numpy as np
    import sys
    import os
    
    def mPlotAndSave(x, y):
        plt.scatter(x, y)
        plt.savefig('mtmp.png')
        plt.clf()
    
    def gPlotAndSave(data, g):
        g("set output 'gtmp.png'")
        g.plot(data)
        g("clear")
        
    def cleanup():
        try:
            os.remove('gtmp.png')
        except OSError:
            pass
        try:
            os.remove('mtmp.png')
        except OSError:
            pass
    
    begin = 2
    end = 500000
    step = 10000
    numberOfPoints = range(begin, end, step)
    n = len(numberOfPoints)
    gnuplotTime = []
    matplotlibTime = []
    progressBarWidth = 30
    
    # Init Gnuplot
    g = Gnuplot.Gnuplot()
    g("set terminal png size 640,480")
    
    # Init matplotlib to avoid a peak in the beginning
    plt.clf()
    
    for idx, val in enumerate(numberOfPoints):
        # Print a nice progress bar (crucial)
        sys.stdout.write('\r')
        progress = (idx+1)*progressBarWidth/n
        bar = "▕" + "▇"*progress + "▁"*(progressBarWidth-progress) + "▏" + str(idx) + "/" + str(n-1)
        sys.stdout.write(bar)
        sys.stdout.flush()
        
        # Generate random data
        x = np.random.randint(sys.maxint, size=val)  
        y = np.random.randint(sys.maxint, size=val)
        gdata = zip(x,y)
        
        # Generate string call to a matplotlib plot and save, call it and save execution time
        start = timer()
        mPlotAndSave(x, y)
        end = timer()
        matplotlibTime.append(end - start)
        
        # Generate string call to a gnuplot plot and save, call it and save execution time
        start = timer()
        gPlotAndSave(gdata, g)
        end = timer()
        gnuplotTime.append(end - start)
        
        # Clean up the files
        cleanup()
    
    del g
    sys.stdout.write('\n')
    plt.plot(numberOfPoints, gnuplotTime, label="gnuplot")
    plt.plot(numberOfPoints, matplotlibTime, label="matplotlib")
    plt.legend(loc='upper right')
    plt.xlabel('Number of points in the scatter graph')
    plt.ylabel('Execution time (s)')
    plt.savefig('execution.png')
    plt.show()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

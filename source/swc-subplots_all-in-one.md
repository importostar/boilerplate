---
title: swc subplots_all in one
date: 2020-05-07
---
Example Python program swc-subplots_all-in-one.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import numpy
* import matplotlib.pyplot
* import glob

## Code

Python example

    import numpy
    import matplotlib.pyplot
    import glob
    
    filenames = glob.glob('inflammation*.csv')
    #filenames = filenames[0:3]
    
    fig = matplotlib.pyplot.figure(figsize=(10.0, 4.0))
    
    axes1 = fig.add_subplot(1, 4, 1)
    axes2 = fig.add_subplot(1, 4, 2)
    axes3 = fig.add_subplot(1, 4, 3)
    
    axes1.set_ylabel('average')
    axes2.set_ylabel('max')
    axes3.set_ylabel('min')
    
    for f in filenames:
        print(f)
    
        data = numpy.loadtxt(fname=f, delimiter=',')
    
        if data.max(axis=0)[0] == 0 and data.max(axis=0)[20] == 20:
            print('Suspicious looking maxima!')
        elif data.min(axis=0).sum() == 0:
            print('Minima add up to zero!')
        else:
            print('Seems OK!')
    
        #fig = matplotlib.pyplot.figure(figsize=(10.0, 3.0))
    
        #axes1 = fig.add_subplot(1, 3, 1)
        #axes2 = fig.add_subplot(1, 3, 2)
        #axes3 = fig.add_subplot(1, 3, 3)
    
        #axes1.set_ylabel('average')
        axes1.plot(data.mean(axis=0), label=f)
    
        #axes2.set_ylabel('max')
        axes2.plot(data.max(axis=0), label=f)
    
        #axes3.set_ylabel('min')
        axes3.plot(data.min(axis=0), label=f)
    
        #fig.tight_layout()
    
    #matplotlib.pyplot.legend()
    fig.tight_layout()
    matplotlib.pyplot.legend(bbox_to_anchor=(1.05, 1), loc=2, borderaxespad=0.)
    matplotlib.pyplot.show(fig)

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

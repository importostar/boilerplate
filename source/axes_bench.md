---
title: axes_bench
date: 2020-05-07
---
Example Python program axes_bench.py
For Python version 2.x.
To test your Python version use:

    python --version

## Modules

* import matplotlib
* import matplotlib.pyplot as plt
* import thin_axes
* import time
* import numpy as np
* import platform

## Methods

* def plot(axes):

## Code

Python example

    #!/usr/bin/env python
    #coding=utf-8
    
    import matplotlib
    matplotlib.use("Agg")
    import matplotlib.pyplot as plt
    import thin_axes
    
    import time
    import numpy as np
    
    import platform
    
    print " ".join(platform.uname())
    
    def plot(axes):
        for a in axes.flatten():
            x, y = np.random.randn(2, 5000)
            a.plot(x, y, '.')
    
    
    start_time = time.time()
    fig, axes = plt.subplots(20,20)
    plt.savefig('test.png')
    print "Standard axes {} s".format(time.time() - start_time)
    plt.close()
    
    start_time = time.time()
    fig, axes = plt.subplots(20,20, subplot_kw=dict(projection='thin'))
    plt.savefig('test.png')
    print "Thin axes {} s".format(time.time() - start_time)
    plt.close()
    
    start_time = time.time()
    fig, axes = plt.subplots(20,20)
    plt.savefig('test.png')
    print "Standard axes with plotting {} s".format(time.time() - start_time)
    plt.close()
    
    start_time = time.time()
    fig, axes = plt.subplots(20,20, subplot_kw=dict(projection='thin'))
    plot(axes)
    plt.savefig('test.png')
    print "Thin axes with plotting {} s".format(time.time() - start_time)
    plt.close()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

---
title: test_pyplot (1)
date: 2020-05-07
---
Example Python program test_pyplot (1).py

## Modules

* import matplotlib as mpl
* import matplotlib.pyplot as plt
* import numpy as np
* import guppy

## Code

Python example

    
    # Original
    #
    # Memory usage (iteration, object count, memory size)
    # 100 431941 134768552
    # 200 862736 269479552
    # 300 1295682 405239168
    # 400 1726603 539967136
    # 500 2157948 674784872
    # 600 2589067 809598080
    # 700 3020848 944697920
    # 800 3451516 1079398704
    # 900 3884074 1214923736
    # 
    # 2542.85 real      2535.49 user         6.66 sys
    
    import matplotlib as mpl
    mpl.use('Agg')
    import matplotlib.pyplot as plt
    
    import numpy as np
    
    import guppy
    
    heapy = guppy.hpy()
    
    mem = open('memory_pyplot.txt', 'wb')
    
    heapy.setref()
    
    for i in range(1000):
    
        if i % 100 == 0:
            h = heapy.heap()
            mem.write('%i %s %s\n' % (i, h.count, h.size))
    
        fig = plt.figure()
        ax = fig.add_subplot(1, 1, 1)
        ax.scatter(np.random.random(10), np.random.random(10))
        fig.savefig('test.png')
    
        mem.flush()
    
    mem.close()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

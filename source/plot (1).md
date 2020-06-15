---
title: plot (1)
date: 2020-05-07
---
Example Python program plot (1).py

## Modules

* import sys, os
* import numpy as np
* import matplotlib
* import csv
* from scipy import interpolate
* import matplotlib.pyplot as plt
* import matplotlib.cm as cm
* from matplotlib.ticker import EngFormatter

## Code

Python example

    #!/usr/bin/env python
    
    import sys, os
    
    import numpy as np
    import matplotlib
    import csv
    from scipy import interpolate
    
    import matplotlib.pyplot as plt
    import matplotlib.cm as cm
    from matplotlib.ticker import EngFormatter
    
    data = np.loadtxt('roo.dat')
    ind = data[0:7, 0]
    lind = np.log10(ind)
    xnew = np.arange(min(lind),max(lind),0.01)
    
    results = []
    y = []
    s = 0
    for i in range(0, 6):
        results.append(data[s:s+7, 1])
        tck = interpolate.splrep(lind,results[i],s=1)
        y.append(interpolate.splev(xnew,tck,der=0))
        s = s + 7
    
    fig, ax = plt.subplots()
    ax.grid(True)
    axes = plt.gca()
    plt.xscale('log')
    axes.set_xlim([5, max(ind) + 0.5*10**7])
    axes.set_ylim([0, max(data[:, 1] * 1.2)])
    khash = plt.plot(ind, results[0], 'o', [10**x for x in xnew], y[0], '-', label='C-KHash', c='blue')
    jahash = plt.plot(ind, results[1], 'v', [10**x for x in xnew], y[1], '-', label='C-Jahash', c='red')
    uthash = plt.plot(ind, results[2], 'H', [10**x for x in xnew], y[2], '-', c='green')
    umap = plt.plot(ind, results[3], '^', [10**x for x in xnew], y[3], '-', c='magenta')
    jmap = plt.plot(ind, results[4], '*', [10**x for x in xnew], y[4], '-', c='cyan')
    luamap = plt.plot(ind, results[5], 'd', [10**x for x in xnew], y[5], '-', c='yellow')
    plt.ylabel('Lookups(millions per second)')
    plt.xlabel('Elements in hash table')
    
    plt.legend([khash[0],jahash[0],uthash[0],umap[0],jmap[0],luamap[0]], ['C-khash', 'C-jahash', 'C-uthash', 'C++-unordered_map', 'Java-HashMap', 'LuaJIT-builtin'])
    
    plt.tight_layout()
    plt.show()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

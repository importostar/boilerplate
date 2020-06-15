---
title: test_python (1)
date: 2020-05-07
---
Example Python program test_python (1).py

## Modules

* # import packages installed that are necessary for this exercise
* import numpy as np
* import matplotlib
* import matplotlib.pyplot as plt

## Code

Python example

    # import packages installed that are necessary for this exercise
    import numpy as np
    import matplotlib
    import matplotlib.pyplot as plt
    
    # set up display of plot in Jupyter Notebook
    %matplotlib inline
    matplotlib.rcParams['figure.figsize'] = (12,8)
    
    # example from matplotlib website - https://matplotlib.org/gallery/lines_bars_and_markers/bar_stacked.html#sphx-glr-gallery-lines-bars-and-markers-bar-stacked-py
    N = 5
    menMeans = (20, 35, 30, 35, 27)
    womenMeans = (25, 32, 34, 20, 25)
    menStd = (2, 3, 4, 1, 2)
    womenStd = (3, 5, 2, 3, 3)
    ind = np.arange(N)    # the x locations for the groups
    width = 0.35       # the width of the bars: can also be len(x) sequence
    
    p1 = plt.bar(ind, menMeans, width, yerr=menStd)
    p2 = plt.bar(ind, womenMeans, width,
                 bottom=menMeans, yerr=womenStd)
    
    plt.ylabel('Scores')
    plt.title('Scores by group and gender')
    plt.xticks(ind, ('G1', 'G2', 'G3', 'G4', 'G5'))
    plt.yticks(np.arange(0, 81, 10))
    plt.legend((p1[0], p2[0]), ('Men', 'Women'))
    
    plt.show()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

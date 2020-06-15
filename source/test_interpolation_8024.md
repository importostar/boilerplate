---
title: test_interpolation_8024
date: 2020-05-07
---
Example Python program test_interpolation_8024.py

## Modules

* import matplotlib as mpl
* import matplotlib.pyplot as plt
* import matplotlib.colors as mcolors
* import matplotlib.image as mimage
* import matplotlib.cm as mcm
* import numpy as np
* import copy

## Code

Python example

    #notes: figure out matplotlib/agg image interpolation
    # start with src/_image_resample.h:resample(...)
    # agg_span_image_filter_gray.h / very end: -> clipping
    
    import matplotlib as mpl
    mpl.use('agg')
    
    import matplotlib.pyplot as plt
    import matplotlib.colors as mcolors
    import matplotlib.image as mimage
    import matplotlib.cm as mcm
    import numpy as np
    import copy
    
    #cm = copy.copy(mcm.get_cmap('viridis'))
    cm = copy.copy(mcm.get_cmap('gray'))
    cm.set_over('r')
    cm.set_under('c')
    cm.set_bad('k')
    
    n = mcolors.Normalize(vmin=0, vmax=100)
    
    data = np.arange(100, dtype='float').reshape(10, 10)
    
    data[7, 3] = -10
    data[3, 7] = 200
    data[3, 8] = -100
    data[7, 7] = 110
    data[9, 0] = 101
    data[3,3] = 1000
    
    
    #data[3, 3] = np.nan
    #data[5, 3] = np.inf
    
    mask = np.zeros_like(data).astype('bool')
    #mask[3, 5] = True
    
    data = np.ma.masked_array(data, mask)
    
    fig, ax_grid = plt.subplots(3, 6, figsize=(12,6))
    for interp, ax in zip(mimage._interpd_, ax_grid.ravel()):
        ax.set_title(interp)
        im = ax.imshow(data, norm=n, cmap=cm, interpolation=interp)
        ax.axis('off')
    
    plt.tight_layout( )
    plt.savefig('test_interpolation_8024.png', dpi=72)
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

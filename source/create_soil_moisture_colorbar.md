---
title: create_soil_moisture_colorbar
date: 2020-05-07
---
Example Python program create_soil_moisture_colorbar.py

## Modules

* import matplotlib
* import matplotlib.pyplot as plt
* import numpy as np
* from matplotlib.colors import LinearSegmentedColormap

## Code

Python example

    import matplotlib
    matplotlib.use('agg')
    matplotlib.rcdefaults()
    
    import matplotlib.pyplot as plt
    
    height = 500
    width = 150
    
    import numpy as np
    
    from matplotlib.colors import LinearSegmentedColormap
    cmap = LinearSegmentedColormap.from_list('sm', ((1,0.95,0.7), (0.9,0.75,0.6), (0.3,0.5,1), (0,0,0.4)), N=60)
    
    dpi = 150
    size = (width/dpi, height/dpi)
    fig = plt.figure(1, size, dpi=dpi)
    
    arr = np.ones((10,10))/float(2)
    arr[0,0] = 0
    
    ax = plt.axes(frameon=False)
    ax.get_xaxis().tick_bottom()
    ax.get_xaxis().set_visible(False)
    ax.get_yaxis().set_visible(False)
    im = ax.imshow(arr, cmap=cmap)
    ax.cla()
    
    cbax = fig.add_axes([0.08, 0.05, 1, 0.9])
    cbax.set_axis_off()
    cb = plt.colorbar(im, ax=cbax, fraction = 1, aspect = 8, label = 'cm$^3$ cm$^-3$', spacing = 'proportional')
    cb.set_ticks([0, 0.1, 0.2, 0.3, 0.4, 0.5])
    
    fig.savefig('vwc_colorbar.png', dpi=dpi)

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

---
title: circular_colormap_mwe
date: 2020-05-07
---
Example Python program circular_colormap_mwe.py

## Modules

* # default matplotlib imports
* import matplotlib as mpl
* import matplotlib.pyplot as plt
* from matplotlib.colors import Normalize
* from matplotlib.cm import ScalarMappable
* from mpl_toolkits.axes_grid1 import make_axes_locatable
* import numpy as np

## Code

Python example

    # default matplotlib imports
    import matplotlib as mpl
    import matplotlib.pyplot as plt
    
    # colormap
    from matplotlib.colors import Normalize
    from matplotlib.cm import ScalarMappable
    cmap = plt.cm.hsv # colormap (plt.cm.hsv = circular colormap)
    
    # colormap bar
    from mpl_toolkits.axes_grid1 import make_axes_locatable
    
    #####
    
    # data
    import numpy as np
    thetas = np.linspace(0, 2*np.pi, 100)
    
    #####
    
    # colormap
    norm = Normalize(           # definition of norm
    	vmin=0,                   # minimum value
    	vmax=2*np.pi)             # maximum value
    scalarMap = ScalarMappable( # define relation from numerical value to color
    	norm=norm,                # norm defined above
    	cmap=cmap)                # colormap
    
    # figure
    fig, ax = plt.subplots()
    for theta in thetas:
    	ax.scatter(np.cos(theta), np.sin(theta), marker='.', s=10,
    		color=scalarMap.to_rgba(theta)) # use scalarMap to get color from numerical value
    
    # colormap bar
    colormap_ax = make_axes_locatable(ax).append_axes('right', size='5%', pad=0.05) # colormap bar axis
    colormap_bar = mpl.colorbar.ColorbarBase(                                       # colormap map bar
    	colormap_ax, cmap=cmap, norm=norm, orientation='vertical')
    
    # show
    plt.show()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

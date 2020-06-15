---
title: surface3d_demo
date: 2020-05-07
---
Example Python program surface3d_demo.py

## Modules

* import numpy as np
* import matplotlib.pyplot as plt
* from matplotlib import rcParams
* from matplotlib.ticker import LinearLocator

## Code

Python example

    import numpy as np
    
    import matplotlib.pyplot as plt
    from matplotlib import rcParams
    from matplotlib.ticker import LinearLocator
    
    # use default Latex font for math even with matplotlib 2.0
    rcParams['mathtext.fontset'] = 'cm'
    
    fig = plt.figure()
    ax = fig.gca(projection='3d')
    
    # set the limits
    xlim = (-2, 2)
    ylim = (0, 2)
    zlim = (0, 2)
    
    # Make data.
    Y = np.linspace(ylim[0], ylim[1], 30)
    Z = np.linspace(zlim[0], zlim[1], 30)
    Z, Y = np.meshgrid(Z, Y)
    
    X = np.sqrt(Z * Y)
    
    # Plot the surface.
    for x in [X, -X]:
        surf = ax.plot_surface(x, Y, Z, rstride=1, cstride=1,
                               shade=False, edgecolor='k', color='w',
                               linewidth=0.5, antialiased=True)
    
    ax.set_xlim(xlim)
    ax.set_ylim(ylim)
    ax.set_zlim(zlim)
    ax.xaxis.set_major_locator(LinearLocator(3))
    ax.yaxis.set_major_locator(LinearLocator(3))
    ax.zaxis.set_major_locator(LinearLocator(3))
    
    # rotate view
    ax.azim, ax.elev = -135, 20
    
    ax.set(xlabel=r'$x$', ylabel=r'$y$', zlabel=r'$f(x,y)$')
    ax.set(title=r'Figure 3.3 - Graph of $f(x,y)=x^2/y$')
    ax.grid('off')
    
    plt.show()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

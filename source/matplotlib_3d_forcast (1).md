---
title: matplotlib_3d_forcast (1)
date: 2020-05-07
---
Example Python program matplotlib_3d_forcast (1).py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import matplotlib.pyplot as plt
* import numpy as np

## Code

Python example

    """
    Demonstrates similarities between pcolor, pcolormesh, imshow and pcolorfast
    for drawing quadrilateral grids.
    """
    import matplotlib.pyplot as plt
    import numpy as np
    
    
    data = np.loadtxt(open("data.csv","rb"),delimiter=",",skiprows=0)
    data=data.transpose()
    print(type(data.shape))
    # make these smaller to increase the resolution
    dy,dx = 1,5
    
    
    # generate 2 2d grids for the x & y bounds
    y, x = np.mgrid[
                    slice(0,5995 , dx),slice(0, data.shape[1] , dy)]
    
    print(x)
    print('---------------------')
    
    print(y)
    z = data#(1 - x / 2. + x ** 5 + y ** 3) * np.exp(-x ** 2 - y ** 2)
    # x and y are bounds, so z should be the value *inside* those bounds.
    # Therefore, remove the last value from the z array.
    z = z[:-1, :-1]
    z_min, z_max = -np.abs(z).max(), np.abs(z).max()
    
    # plt.subplot(2, 2, 1)
    
    print(x)
    print(y)
    print(z)
    
    plt.pcolor(x, y, z, cmap='hot', vmin=0, vmax=z_max)
    plt.title('Cloud')
    # set the limits of the plot to the limits of the data
    plt.axis([0, x.max(), 0, y.max()])
    plt.colorbar()
    
    plt.subplots_adjust(wspace=0.5, hspace=0.5)
    
    plt.show()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

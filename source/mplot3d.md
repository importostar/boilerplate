---
title: mplot3d
date: 2020-05-07
---
Example Python program mplot3d.py

## Modules

* from mpl_toolkits.mplot3d import Axes3D
* from matplotlib import cm
* from matplotlib.ticker import LinearLocator, FormatStrFormatter
* import matplotlib.pyplot as plt
* import numpy as np
* from mpl_toolkits.mplot3d import Axes3D
* import numpy as np
* import matplotlib
* import matplotlib.pyplot as plt
* import numpy as np
* from mpl_toolkits.mplot3d import Axes3D
* import matplotlib.pyplot as plt

## Methods

* def randrange(n, vmin, vmax):

## Code

Python example

    
    
    #Gráficos 3D
    from mpl_toolkits.mplot3d import Axes3D
    from matplotlib import cm
    from matplotlib.ticker import LinearLocator, FormatStrFormatter
    import matplotlib.pyplot as plt
    import numpy as np
    
    fig = plt.figure()
    ax = fig.gca(projection='3d')
    X = np.arange(-5, 5, 0.25)
    Y = np.arange(-5, 5, 0.25)
    X, Y = np.meshgrid(X, Y)
    R = np.sqrt(X**2 + Y**2)
    Z = np.sin(R)
    surf = ax.plot_surface(X, Y, Z, rstride=1, cstride=1, cmap=cm.jet,
            linewidth=0, antialiased=False)
    
    fig.colorbar(surf, shrink=0.5, aspect=5)
    
    plt.show()
    
    
    #Gráficos 3D (linha)
    
    from mpl_toolkits.mplot3d import Axes3D
    import numpy as np
    import matplotlib
    import matplotlib.pyplot as plt
    
    fig = plt.figure()
    ax = Axes3D(fig)
    
    x = [6,3,6,9,12,24]
    y = [3,5,78,12,23,56]
    # put 0s on the y-axis, and put the y axis on the z-axis
    ax.plot(xs=x, ys=[0]*len(x), zs=y, zdir='z', label='ys=0, zdir=z')
    plt.show()
    
    
    
    #Scatter plots em 3D
    import numpy as np
    from mpl_toolkits.mplot3d import Axes3D
    import matplotlib.pyplot as plt
    
    def randrange(n, vmin, vmax):
        return (vmax-vmin)*np.random.rand(n) + vmin
    
    fig = plt.figure()
    ax = fig.add_subplot(111, projection='3d')
    n = 100
    for c, m, zl, zh in [('r', 'o', -50, -25), ('b', '^', -30, -5)]:
        xs = randrange(n, 23, 32)
        ys = randrange(n, 0, 100)
        zs = randrange(n, zl, zh)
        ax.scatter(xs, ys, zs, c=c, marker=m)
    
    ax.set_xlabel('X Label')
    ax.set_ylabel('Y Label')
    ax.set_zlabel('Z Label')
    
    plt.show()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

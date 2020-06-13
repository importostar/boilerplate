---
title: myplot
date: 2020-05-07
---
Example Python program myplot.py

## Modules

* import matplotlib
* matplotlib.use('Agg') # Must be before importing matplotlib.pyplot or pylab!
* from mpl_toolkits.mplot3d import Axes3D, axes3d
* import matplotlib.pyplot as plt
* import numpy as np

## Code

Python example

    import matplotlib
    matplotlib.use('Agg') # Must be before importing matplotlib.pyplot or pylab!
    from mpl_toolkits.mplot3d import Axes3D, axes3d
    import matplotlib.pyplot as plt
    import numpy as np
    
    # center and radius
    center = [0,0,0]
    radius = 4
    angle =0# np.pi /8
    # data
    u = np.linspace(0 + angle, 2 * np.pi + angle, 100)
    v = np.linspace(0, np.pi, 100)
    x = radius * np.outer(np.cos(u), np.sin(v)) + center[0]
    y = radius * np.outer(np.sin(u), np.sin(v)) + center[1]
    z = radius * np.outer(np.ones(np.size(u)), np.cos(v)) + center[2]
    
    
    # plot
    fig = plt.figure(figsize= (6,6))
    ax = fig.add_subplot(111, projection='3d')
    ax.set_zlabel('Z') #坐标轴
    ax.set_ylabel('Y')
    ax.set_xlabel('X')
    
    ax.set_xlim(-5,5)
    ax.set_ylim(-5,5)
    ax.set_zlim(-5,5)
    # ax = fig.add_subplot(111, projection='3d')
    # # surface plot
    # ax.plot_surface(x, y, z,  rstride=4, cstride=4, color='b')
    
    #wire frame
    ax.plot_wireframe(x, y, z, rstride=10, cstride=10)
    
    
    # show
    plt.show()
    #plt.savefig('sphere.png',format = 'png', dpi = 300)
    #plt.close()
    
    
    
    
    
    
    
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

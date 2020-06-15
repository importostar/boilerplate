---
title: matplotlib_3d_cone2
date: 2020-05-07
---
Example Python program matplotlib_3d_cone2.py

## Modules

* from mpl_toolkits.mplot3d import axes3d
* import matplotlib.pyplot as plt
* from matplotlib import cm
* import numpy as np

## Code

Python example

    from mpl_toolkits.mplot3d import axes3d
    import matplotlib.pyplot as plt
    from matplotlib import cm
    import numpy as np
    
    fig = plt.figure()
    ax = fig.add_subplot(111, projection='3d')
    
    # Set up the grid in polar
    beta = np.linspace(0, 2 * np.pi, 360)
    r = np.arange(0, 3000, 5)
    Beta, R = np.meshgrid(beta, r)
    alpha = np.pi * 0.25  # 仰角45度
    # Then calculate X, Y, and Z
    X = R * np.cos(Beta)
    Y = R * np.sin(Beta)
    Z = 0.9 * np.sqrt(X ** 2 + Y ** 2)
    
    data = np.loadtxt(open("data5.csv", "rb"), delimiter=",", skiprows=0)  # 读取矩阵数据
    data = data[:, 0:600]  # 取前600列，即3000m
    
    dataT = data.T
    
    N = dataT
    cmp = cm.jet(N)
    surf = ax.plot_surface(X, Y, Z, rstride=1, cstride=1, facecolors=cmp, linewidth=0, antialiased=True)
    ax.set_xlabel("X")
    ax.set_ylabel("Y")
    ax.set_zlabel("Hight/m")
    # ax.set_zlim(0,2)
    
    m = cm.ScalarMappable(cmap=cm.jet)
    m.set_array(N)
    plt.colorbar(m)
    
    plt.show()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

---
title: TwoVariableFunc
date: 2020-05-07
---
Example Python program TwoVariableFunc.py

## Modules

* import matplotlib.pyplot as plt
* import numpy as np
* from mpl_toolkits.mplot3d import Axes3D

## Methods

* def ExFunc(x, y):
* def FuncPlot2(f, x, y):

## Code

Python example

    import matplotlib.pyplot as plt
    import numpy as np
    from mpl_toolkits.mplot3d import Axes3D
    
    
    def ExFunc(x, y):
        return -x ** 2-y ** 2+1
    
    
    def FuncPlot2(f, x, y):
        out = np.zeros((len(x), len(y)))
        for i_y, p_y in enumerate(y):
            for i_x, p_x in enumerate(x):
                out[i_x, i_y] = f(p_x, p_y)
        return out
    
    
    Interval = np.array([-5, 5])
    Nsamp = 100
    x = np.linspace(-5, 5, Nsamp)
    y = np.linspace(-5, 5, Nsamp)
    h = FuncPlot2(ExFunc, x, y)
    
    X, Y = np.meshgrid(x, y)
    
    figure = plt.figure()
    ax = figure.add_subplot(111, projection='3d')
    ax.set_xlabel("x", size=14)
    ax.set_ylabel("y", size=14)
    ax.set_zlabel("h", size=14)
    surf = ax.plot_surface(X, Y, h, cmap="bwr", linewidth=0)
    figure.colorbar(surf)
    ax.set_title("TwoVariableFunc")
    plt.show()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

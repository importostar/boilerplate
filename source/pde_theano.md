---
title: pde_theano
date: 2020-05-07
---
Example Python program pde_theano.py

## Modules

* import matplotlib
* import matplotlib.pyplot as plt
* import numpy as np
* import time
* from mpl_toolkits.mplot3d import Axes3D
* from matplotlib import cm
* import theano as th
* from theano import tensor as T

## Methods

* def draw_plot(x, y, U):
* def pde_step(U):

## Code

Python example

    import matplotlib
    import matplotlib.pyplot as plt
    import numpy as np
    import time
    from mpl_toolkits.mplot3d import Axes3D
    from matplotlib import cm
    
    import theano as th
    from theano import tensor as T
    
    
    plt.ion()
    fig = plt.figure()
    ax = fig.add_subplot(111, projection='3d')
    ax.set_zlim(-1.01, 1.01)
    
    
    def draw_plot(x, y, U):
        ax.clear()
        ax.set_zlim(-1.01, 1.01)
        ax.plot_surface(x, y, U, rstride=1, cstride=1, cmap=cm.coolwarm,
                        linewidth=0, antialiased=True)
        plt.pause(1e-5)
    
    
    # Create 21x21 mesh grid
    m = 21
    mesh_range = np.arange(-1, 1, 2/(m-1))
    x_arr, y_arr = np.meshgrid(mesh_range, mesh_range)
    
    # Initialize variables
    x, y = th.shared(x_arr), th.shared(y_arr)
    U = T.exp(-5 * (x**2 + y**2))
    
    draw_plot(x_arr, y_arr, U.eval())
    
    n = list(range(1, m-1)) + [m-2]
    e = n
    s = [0] + list(range(0, m-2))
    w = s
    
    
    def pde_step(U):
        """ PDE calculation at a single time step t  """
        return (U[n, :]+U[:, e]+U[s, :]+U[:, w])/4.
    
    
    k = 5
    
    # Batch process the PDE calculation, calculate together k steps
    result, updates = th.scan(fn=pde_step, outputs_info=U, n_steps=k)
    final_result = result[-1]
    calc_pde = th.function(inputs=[U], outputs=final_result, updates=updates)
    
    U_step = U.eval()
    
    for it in range(100):
        # Every k steps, draw the graphics
        U_step = calc_pde(U_step)
        draw_plot(x_arr, y_arr, U_step)
    
    while True:
        plt.pause(1e-5)
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

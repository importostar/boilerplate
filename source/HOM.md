---
title: HOM
date: 2020-05-07
---
Example Python program HOM.py

## Modules

* import numpy as np
* import math
* import os
* import random
* import matplotlib.pyplot as plt
* import matplotlib
* import functools
* import itertools
* from matplotlib.animation import FuncAnimation

## Methods

* def get_derivative(fc, x_1, eps=1e-5):
* def gradiend_descent(func, x_0, n_iter=1000, mu=lambda n: 0.01 / n ** 0.5) :
* def HOM( final_function, start_function, x_0, n_steps=10):
* def complex_function(x):
* def simple_function(x):

## Code

Python example

    import numpy as np
    import math
    import os
    import random
    import matplotlib.pyplot as plt
    import matplotlib
     
    %matplotlib inline
     
     
    import functools
    import itertools
     
    from matplotlib.animation import FuncAnimation
     
    def get_derivative(fc, x_1, eps=1e-5):
        res = []
        x_t = x_1[:]
        for i in range(len(x_1)):
            x_t[i] += eps
            res.append( (fc(x_t) - fc(x_1)) / eps)
            x_t[i] -= eps
       
        return res
     
     
    def gradiend_descent(func, x_0, n_iter=1000, mu=lambda n: 0.01 / n ** 0.5) :
       
        x_tmp = x_0[:]
        traj = [x_tmp]
       
        for iteration in range(n_iter):
            delta = get_derivative(func, x_tmp)
            for j in range(len(x_tmp)):
                x_tmp[j] -= mu(iteration + 1) * delta[j]
           
            for i in range(len(x_tmp)):
                if x_tmp[i] > 1:
                    x_tmp[i] = 1
                elif x_tmp[i] < 0:
                    x_tmp[i] = 0
           
            traj.append(x_tmp[:])
           
        return traj
     
    def HOM( final_function, start_function, x_0, n_steps=10):
       
        t_array = np.linspace(0, 1, n_steps + 1)
     
        for t in t_array:
           
            f_tmp = lambda x: (1 - t) * start_function(x) + (t) * final_function(x)
           
            trajectory_current = gradiend_descent(f_tmp, x_0[:], n_iter=10000)
                                                 
            x_0 = trajectory_current[-1][:]
           
            fig = plt.figure(figsize=(6,6))
            ax = fig.add_subplot(111)
           
            l = np.linspace(0, 1, 100)
            xx, yy = np.meshgrid(l, l)
            zz = np.zeros(xx.shape)
            for i in range(zz.shape[0]):
                for j in range(zz.shape[1]):
                    zz[i, j] = f_tmp( [ xx[i, j], yy[i, j] ]  )
           
            ax.contourf(xx, yy, zz)
            tjc = np.array(trajectory_current)
            ax.plot(tjc[:, 0], tjc[:, 1], color='red')
            ax.grid()
            fig.savefig('{}.png'.format(t))
            plt.show()
           
        return x_0[:]
     
    def complex_function(x):
        a, b = x[0], x[1]
        return ( np.sin((a) ** 2) + np.cos(a * b * 5) ** 2 + (2 * a - 0.2) ** 2) / 5 - 1
     
    def simple_function(x):
        a, b = x[0], x[1]
        return (a - 0.9) ** 2 + (b - 0.5) ** 2
       
    if __name__ == "__main__":
        HOM(complex_function, simple_function, [0.2, 0.6], 10)

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

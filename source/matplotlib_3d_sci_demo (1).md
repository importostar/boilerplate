---
title: matplotlib_3d_sci_demo (1)
date: 2020-05-07
---
Example Python program matplotlib_3d_sci_demo (1).py

## Modules

* import scipy.io as sio
* from mpl_toolkits.mplot3d import Axes3D
* import matplotlib.pyplot as plt
* import numpy as np

## Methods

* def Detectionplot():

## Code

Python example

    import scipy.io as sio
    from mpl_toolkits.mplot3d import Axes3D
    import matplotlib.pyplot as plt
    import numpy as np
    
    def Detectionplot():
        data = np.loadtxt(open("data.csv", "rb"), delimiter=",", skiprows=0)
        m = data['data']#将其与m数组形成对应关系
    
        fig = plt.figure()
        ax = fig.add_subplot(111, projection='3d')   #此处因为是要和其他的图像一起展示，用的add_subplot，如果只是展示一幅图的话，可以用subplot即可
    
        x = m[0]
        y = m[1]
        z = m[2]
    
        x = x.flatten('F')   #flatten功能具体可从Declaration中看到
        y = y.flatten('F')
    
    #更改柱形图的颜色，这里没有导入第四维信息，可以用z来表示了
        C = []
        for a in z:
            if a < 10:
                C.append('b')
            elif a < 20:
                C.append('c')
            elif a < 30:
                C.append('m')
            elif a < 40:
                C.append('pink')
            elif a > 39:
                C.append('r')
    
    #此处dx，dy，dz是决定在3D柱形图中的柱形的长宽高三个变量
        dx = 0.6 * np.ones_like(x)
        dy = 0.2 * np.ones_like(y)
        dz = abs(z) * z.flatten()
        dz = dz.flatten() / abs(z)
        z = np.zeros_like(z)
    
    #设置三个维度的标签
        ax.set_xlabel('Xlabel')
        ax.set_ylabel('Ylabel')
        ax.set_zlabel('Amplitude')
    
        ax.bar3d(x, y, z, dx, dy, dz, color=C, zsort='average')
    
        plt.show()
    
    Detectionplot()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

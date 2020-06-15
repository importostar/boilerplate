---
title: matplotlib_3d_2 CloudScanning_Cone (1)
date: 2020-05-07
---
Example Python program matplotlib_3d_2-CloudScanning_Cone (1).py

## Modules

* from mpl_toolkits.mplot3d import axes3d
* import matplotlib.pyplot as plt
* from matplotlib import cm,colors
* import numpy as np

## Code

Python example

    from mpl_toolkits.mplot3d import axes3d
    import matplotlib.pyplot as plt
    from matplotlib import cm,colors
    import numpy as np
    data_from_csv_file = np.loadtxt(open("data6.csv", "rb"), delimiter=",", skiprows=1)  # 读取矩阵数据
    data = data_from_csv_file[:, 5:605]  # 取前600列，即3000m
    
    fig = plt.figure()
    ax = fig.add_subplot(111, projection='3d')
    
    elevations= (data_from_csv_file[:, 4] / 180) * np.pi
    Rotations= data_from_csv_file[:, 3] / 180 * np.pi
    r = np.arange(0, 3000, 5)
    Beta, R = np.meshgrid(elevations, r)
    
    # Then calculate X, Y, and Z
    X = R * np.cos(Beta)
    Y = R * np.sin(Beta)
    Z= np.cos(Rotations) * R
    dataT = data.T
    # maxv=np.max(dataT)
    #对数据进行处理，算法：归一化后乘以2，此算法可能不对。
    
    # for i in range(dataT.shape[0]):
    # 	for j in range(dataT.shape[1]):
    # 		dataT[i,j]=(dataT[i,j]/maxv)*2
    
    cdict = {'red': ((0., 1, 1),
                     (0.05, 1, 1),
                     (0.11, 0, 0),
                     (0.66, 1, 1),
                     (0.89, 1, 1),
                     (1, 0.5, 0.5)),
             'green': ((0., 1, 1),
                       (0.05, 1, 1),
                       (0.11, 0, 0),
                       (0.375, 1, 1),
                       (0.64, 1, 1),
                       (0.91, 0, 0),
                       (1, 0, 0)),
             'blue': ((0., 1, 1),
                      (0.05, 1, 1),
                      (0.11, 1, 1),
                      (0.34, 1, 1),
                      (0.65, 0, 0),
                      (1, 0, 0))}
    my_cmap = colors.LinearSegmentedColormap('my_colormap',cdict,256)
    cmp2=my_cmap(dataT)##使用用户自定义颜色映射方案
    
    #cmp = cm.jet(N)##使用内置颜色映射方案
    # surf = ax.plot_surface(X, Y, Z, rstride=10, cstride=10, facecolors=cmp2, linewidth=0, antialiased=True)
    ax.plot_surface(X, Y, Z, rstride=1, cstride=1, facecolors=cmp2, linewidth=0, antialiased=True)
    ax.set_xlabel("X/m")
    ax.set_ylabel("Y/m")
    ax.set_zlabel("Hight/m")
    
    #图例:
    m = cm.ScalarMappable(cmap=my_cmap)
    m.set_array(dataT)
    plt.colorbar(m)
    
    plt.show()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

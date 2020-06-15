---
title: plot_structuring_3d_elements
date: 2020-05-07
---
Example Python program plot_structuring_3d_elements.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import numpy as np
* import matplotlib.pyplot as plt
* import matplotlib.ticker as ticker
* from mpl_toolkits.mplot3d import Axes3D
* from skimage.morphology import cube
* import numpy as np
* import matplotlib.pyplot as plt
* import matplotlib.ticker as ticker
* from mpl_toolkits.mplot3d import Axes3D
* from skimage.morphology import octahedron
* import numpy as np
* import matplotlib.pyplot as plt
* import matplotlib.ticker as ticker
* from mpl_toolkits.mplot3d import Axes3D
* from skimage.morphology import ball
* import skimage
* import matplotlib

## Code

Python example

    #cube
    import numpy as np
    import matplotlib.pyplot as plt
    import matplotlib.ticker as ticker
    from mpl_toolkits.mplot3d import Axes3D
    from skimage.morphology import cube
    
    # Generate 2D structuring cube elements.
    struc_2d = {
        "cube(1)": cube(1),
        "cube(2)": cube(2),
        "cube(3)": cube(3),
        "cube(4)": cube(4),
        "cube(5)": cube(5),
        "cube(6)": cube(6)}
    
    # Visualize the elements.
    fig = plt.figure(figsize=(10,6.65))
    
    idx = 1
    for title, struc in struc_2d.items():
        ax = fig.add_subplot(2, 3, idx,projection=Axes3D.name)
        ax.voxels(struc,ec='w')
        ax.xaxis.set_major_locator(ticker.MultipleLocator(1))
        ax.yaxis.set_major_locator(ticker.MultipleLocator(1))
        ax.zaxis.set_major_locator(ticker.MultipleLocator(1))
        ax.grid()
        ax.set(xlim=(-1,struc.shape[0]+1),
               ylim=(-1,struc.shape[0]+1),
               zlim=(-1,struc.shape[0]+1))
        ax.set_title(title)
        ax.set_axisbelow(True)
        idx += 1
    
    fig.tight_layout()
    plt.savefig('cube.png',dpi=100)
    plt.show()
    
    #octahedron
    import numpy as np
    import matplotlib.pyplot as plt
    import matplotlib.ticker as ticker
    from mpl_toolkits.mplot3d import Axes3D
    from skimage.morphology import octahedron
    
    # Generate 2D structuring octahedron elements.
    struc_2d = {
        "octahedron(1)": octahedron(1),
        "octahedron(2)": octahedron(2),
        "octahedron(3)": octahedron(3),
        "octahedron(4)": octahedron(4),
        "octahedron(5)": octahedron(5),
        "octahedron(6)": octahedron(6)}
    
    # Visualize the elements.
    fig = plt.figure(figsize=(12,8))
    
    idx = 1
    for title, struc in struc_2d.items():
        ax = fig.add_subplot(2, 3, idx,projection=Axes3D.name)
        ax.voxels(struc,ec='w',fc='C1')
        ax.xaxis.set_major_locator(ticker.MultipleLocator(1))
        ax.yaxis.set_major_locator(ticker.MultipleLocator(1))
        ax.zaxis.set_major_locator(ticker.MultipleLocator(1))
        ax.grid()
        ax.set(xlim=(-1,struc.shape[0]+1),
               ylim=(-1,struc.shape[0]+1),
               zlim=(-1,struc.shape[0]+1))
        ax.set_title(title)
        ax.set_axisbelow(True)
        idx += 1
    
    fig.tight_layout()
    plt.savefig('octahedron.png',dpi=100)
    plt.show()
    
    #ball
    import numpy as np
    import matplotlib.pyplot as plt
    import matplotlib.ticker as ticker
    from mpl_toolkits.mplot3d import Axes3D
    from skimage.morphology import ball
    
    # Generate 2D structuring ball elements.
    struc_2d = {
        "ball(1)": ball(1),
        "ball(2)": ball(2),
        "ball(3)": ball(3),
        "ball(4)": ball(4),
        "ball(5)": ball(5),
        "ball(6)": ball(6)}
    
    # Visualize the elements.
    fig = plt.figure(figsize=(12,8))
    
    idx = 1
    for title, struc in struc_2d.items():
        ax = fig.add_subplot(2, 3, idx,projection=Axes3D.name)
        ax.voxels(struc,ec='w',fc='C2')
        ax.xaxis.set_major_locator(ticker.MultipleLocator(1))
        ax.yaxis.set_major_locator(ticker.MultipleLocator(1))
        ax.zaxis.set_major_locator(ticker.MultipleLocator(1))
        ax.grid()
        ax.set(xlim=(-1,struc.shape[0]+1),
               ylim=(-1,struc.shape[0]+1),
               zlim=(-1,struc.shape[0]+1))
        ax.set_title(title)
        ax.set_axisbelow(True)
        idx += 1
    
    fig.tight_layout()
    plt.savefig('ball.png',dpi=100)
    plt.show()
    
    #version
    import skimage
    print(skimage.__version__)
    0.16.2
    import matplotlib
    print(matplotlib.__version__)
    3.2.0
    print(np.__version__)
    1.18.1
     

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

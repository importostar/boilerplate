---
title: octahedron_rotate (1)
date: 2020-05-07
---
Example Python program octahedron_rotate (1).py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* from IPython.display import HTML
* import matplotlib.animation as animation
* import numpy as np
* import matplotlib.pyplot as plt
* import matplotlib.ticker as ticker
* from mpl_toolkits.mplot3d import Axes3D
* from skimage.morphology import octahedron
* import skimage
* import matplotlib
* import IPython

## Methods

* def animate(i):

## Code

Python example

    from IPython.display import HTML
    import matplotlib.animation as animation
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
    axes=[]
    for title, struc in struc_2d.items():
        ax = fig.add_subplot(2, 3, idx,projection=Axes3D.name)
        ax.voxels(struc,ec='w',fc='C1')
        #ax.xaxis.set_major_locator(ticker.MultipleLocator(1))
        #ax.yaxis.set_major_locator(ticker.MultipleLocator(1))
        #ax.zaxis.set_major_locator(ticker.MultipleLocator(1))
        ax.grid()
        ax.set(xlim=(-1,struc.shape[0]+1),
               ylim=(-1,struc.shape[0]+1),
               zlim=(-1,struc.shape[0]+1))
        ax.set_title(title)
        ax.set_axisbelow(True)
        idx += 1
        axes.append(ax)
    fig.tight_layout()
    
    def animate(i):
        [axes[j].view_init(elev=30., azim=3.6*i) for j in range(6)]
        return fig,
    
    # Animate
    ani = animation.FuncAnimation(fig, animate,frames=100, interval=100, blit=True)    
    ani.save('rotate_3d_oh.mp4', writer="ffmpeg",dpi=100)
    HTML(ani.to_html5_video())
    
    
    
    #version
    import skimage
    print(skimage.__version__)
    #0.16.2
    import matplotlib
    print(matplotlib.__version__)
    #3.2.0
    import IPython
    print(IPython.__version__)
    #7.13.0

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

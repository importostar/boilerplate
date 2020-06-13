---
title: triplot_anim
date: 2020-05-07
---
Example Python program triplot_anim.py

## Modules

* import matplotlib.pyplot as plt
* import matplotlib.tri as tri
* import numpy as np
* import matplotlib.animation as animation
* from IPython.display import HTML

## Methods

* def update(num):
* def update(num):
* def update(num):

## Code

Python example

    %matplotlib inline
    import matplotlib.pyplot as plt
    import matplotlib.tri as tri
    import numpy as np
    import matplotlib.animation as animation
    from IPython.display import HTML
    x = np.random.rand(27)
    y = np.random.rand(27)
    
    fig, ax = plt.subplots(figsize=(5,5))
    
    def update(num):
        ax.cla()
        ax.set_aspect('equal')
        ax.set(xlim=(0,1),ylim=(0,1))
        triang = tri.Triangulation(x[:3+num], y[:3+num])
        ax.triplot(triang, 'go-', lw=1)
        return fig,
    
    ani = animation.FuncAnimation(fig, update, 25,interval=200, blit=True)
    ani.save('triplot_anim25.mp4', writer="ffmpeg",dpi=100)
    HTML(ani.to_html5_video())
    
    
    
    
    x = np.random.rand(52)
    y = np.random.rand(52)
    
    fig, ax = plt.subplots(figsize=(5,5))
    
    def update(num):
        ax.cla()
        ax.set_aspect('equal')
        ax.set(xlim=(0,1),ylim=(0,1))
        triang = tri.Triangulation(x[:3+num], y[:3+num])
        ax.triplot(triang, 'go-', lw=1)
        return fig,
    
    ani = animation.FuncAnimation(fig, update, 50,interval=200, blit=True)
    ani.save('triplot_anim50.mp4', writer="ffmpeg",dpi=100)
    HTML(ani.to_html5_video())
    
    
    
    
    
    x = np.random.rand(102)
    y = np.random.rand(102)
    
    fig, ax = plt.subplots(figsize=(5,5))
    
    def update(num):
        ax.cla()
        ax.set_aspect('equal')
        ax.set(xlim=(0,1),ylim=(0,1))
        triang = tri.Triangulation(x[:3+num], y[:3+num])
        ax.triplot(triang, 'go-', lw=1)
        return fig,
    
    ani = animation.FuncAnimation(fig, update, 100,interval=200, blit=True)
    ani.save('triplot_anim100.mp4', writer="ffmpeg",dpi=100)
    HTML(ani.to_html5_video())
    
     

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

---
title: breath_square
date: 2020-05-07
---
Example Python program breath_square.py

## Modules

* import numpy as np
* import matplotlib.pyplot as plt
* import matplotlib.animation as animation
* from IPython.display import HTML
* from matplotlib.patches import Rectangle

## Methods

* def update(num):

## Code

Python example

    %matplotlib inline
    import numpy as np
    import matplotlib.pyplot as plt
    import matplotlib.animation as animation
    from IPython.display import HTML
    from matplotlib.patches import Rectangle
    
    # create ini data
    x =[-0.7,0.7,0.7,-0.7,-0.7]
    y =[-0.7,-0.7,0.7,0.7,-0.7]
    
    angles = np.linspace(0,2*np.pi,200)
    size1 = np.linspace(0.8,.3,50)
    size2 = np.linspace(0.3,.8,50)
    size = np.hstack([size1,size2])
    
    def update(num):
        #rotate data
        x_=[]
        y_=[]
        theta = angles[num]
        c, s = np.cos(theta), np.sin(theta)
        for i in range(5):
            rot_x = (x[i] * c) - (y[i] * s)
            rot_y = (x[i] * s) + (y[i] * c)
            x_.append(rot_x)
            y_.append(rot_y)
        rect.set_xy(np.array([x_,y_]).T)
        if num > 99:
            rectan1.set_width(size[num-100])
            rectan1.set_height(size[num-100])
            rectan2.set_width(size[num-100])
            rectan2.set_height(size[num-100])
            rectan3.set_width(size[num-100])
            rectan3.set_height(size[num-100])
            rectan4.set_width(size[num-100])
            rectan4.set_height(size[num-100])
    
    fig, ax = plt.subplots(figsize=(8,8))
    rectan1 = Rectangle((-1,-1),width=.8, height=.8,color='C7',zorder=2)
    ax.add_patch(rectan1)
    rectan2 = Rectangle((-1,1),width=.8, height=.8,angle=270,color='C7',zorder=2)
    ax.add_patch(rectan2)
    rectan3 = Rectangle((1,1),width=.8, height=.8,angle=180,color='C7',zorder=2)
    ax.add_patch(rectan3)
    rectan4 = Rectangle((1,-1),width=.8, height=.8,angle=90,color='C7',zorder=2)
    ax.add_patch(rectan4)
    rect, = ax.fill(x, y, color='C2',zorder=1)
    
    ax.set(xlim=(-1.1,1.1), ylim=(-1.1,1.1))
    ax.axis('off')
    ani = animation.FuncAnimation(fig, update, 200,interval=25)
    HTML(ani.to_html5_video())
    #ani.save('brath_square.mp4', writer="ffmpeg",dpi=100)
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

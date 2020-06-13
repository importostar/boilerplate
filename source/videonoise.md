---
title: videonoise
date: 2020-05-07
---
Example Python program videonoise.py

## Modules

* import numpy as np
* from numpy.random import rand
* import matplotlib
* import matplotlib.pyplot as plt
* from matplotlib.animation import FuncAnimation

## Methods

* def init():
* def update(frame):

## Code

Python example

    #! /usr/bin/python3
    
    import numpy as np
    from numpy.random import rand
    import matplotlib
    
    matplotlib.use('Qt5Agg')
    import matplotlib.pyplot as plt
    from matplotlib.animation import FuncAnimation
    
    WIDTH, HEIGHT = 1200, 600
    
    fig, ax = plt.subplots()
    
    # the following lines are just for better look and not essential
    ax.set_axis_off()
    fig.set_facecolor('k')
    fig.set_tight_layout({'pad': 0.0})
    
    empty_screen = np.zeros((HEIGHT, WIDTH, 3))
    screen = np.zeros((HEIGHT, WIDTH, 3))
    img = ax.imshow(empty_screen)
    
    
    def init():
        img.set_data(empty_screen)
        return (img,)
    
    
    def update(frame):
        noise = rand(HEIGHT, WIDTH)
        for i in range(3):
            screen[:, :, i] = noise
        img.set_data(screen)
        return (img,)
    
    
    # using `blit` or not shouldn't make much difference here
    anim = FuncAnimation(fig, update, None, init, blit=True, interval=50)
    plt.show()
    
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

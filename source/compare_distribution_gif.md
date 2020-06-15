---
title: compare_distribution_gif
date: 2020-05-07
---
Example Python program compare_distribution_gif.py

## Modules

* import sys
* import numpy as np
* import matplotlib as mpl
* import matplotlib.pyplot as plt
* import seaborn as sns
* import imageio
* from matplotlib.animation import FuncAnimation
* import matplotlib.animation as animation

## Methods

* def update(i):

## Code

Python example

    import sys
    import numpy as np
    import matplotlib as mpl
    mpl.use('Agg')
    import matplotlib.pyplot as plt
    plt.clf()
    import seaborn as sns
    import imageio
    from matplotlib.animation import FuncAnimation
    import matplotlib.animation as animation
    
    
    def update(i):
        plt.clf()
        sns.distplot(p1[i], label='1')
        sns.distplot(p2[i], label='2')
        plt.xlabel("x label")
        plt.legend(loc='lower right')
        ax = plt.gca()
    
        ax.figure.canvas.draw()       # draw the canvas, cache the renderer
        image = np.frombuffer(ax.figure.canvas.tostring_rgb(), dtype='uint8')
        image = image.reshape(ax.figure.canvas.get_width_height()[::-1] + (3,))
        return image
    
    
    p1 = np.load('1.npy')
    p2 = np.load('2.npy')
    fig = plt.figure(figsize=(10, 6))
    
    images = []
    for i in range(p1.shape[0]):
        images.append(update(i))
    
    images = np.array(images)
    
    kwargs_write = {'fps': 1.0, 'quantizer': 'nq'}
    imageio.mimsave('test.gif', images, fps=1)
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

---
title: d_cousor
date: 2020-05-07
---
Example Python program d_cousor.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import numpy as np
* import matplotlib.pyplot as plt
* import matplotlib

## Classes

* class DoubleCursor(object):

## Methods

* def __init__(self, ax,ax2):
* def mouse_move(self, event):

## Code

Python example

    %matplotlib
    import numpy as np
    import matplotlib.pyplot as plt
    plt.rcParams['font.size']=14
    
    class DoubleCursor(object):
        def __init__(self, ax,ax2):
            self.ax = ax
            self.ax2 = ax2
            self.lx = ax.axhline(color='pink')  # the horiz line
            self.ly = ax.axvline(color='pink')  # the vert line
            self.lx2 = ax2.axhline(color='pink')  # the horiz line
            self.ly2 = ax2.axvline(color='pink')  # the vert line
            
        def mouse_move(self, event):
            if not event.inaxes:
                return
    
            x, y = event.xdata, event.ydata
            # update the line positions
            self.lx.set_ydata(y)
            self.ly.set_xdata(x)
            self.lx2.set_ydata(y)
            self.ly2.set_xdata(x)
            #update text
            self.ax.set_title('x=%1.2f, y=%1.2f' % (x, y))
            self.ax2.set_title('x=%1.2f, y=%1.2f' % (x, y))
            self.ax.figure.canvas.draw()
            self.ax2.figure.canvas.draw()
    
    fig,axes = plt.subplots(figsize=(8, 4),ncols=2)
    ax=axes[0]
    ax2=axes[1]
    data = np.random.rand(5,5)
    ax.imshow(data,origin="lower",cmap='cividis')
    data2 = np.random.rand(5,5)
    ax2.imshow(data2,origin="lower",cmap='cividis')
    
    d_cursor = DoubleCursor(ax,ax2)
    fig.canvas.mpl_connect('motion_notify_event', d_cursor.mouse_move)
    
    
    #version
    import matplotlib
    print(matplotlib.__version__)
    print(np.__version__)
    #3.2.0
    #1.18.1

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

---
title: SnaptoCursor
date: 2020-05-07
---
Example Python program SnaptoCursor.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import numpy as np
* import matplotlib.pyplot as plt
* import matplotlib

## Classes

* class SnaptoCursor(object):

## Methods

* def __init__(self, ax, x, y):
* def mouse_move(self, event):

## Code

Python example

    %matplotlib
    import numpy as np
    import matplotlib.pyplot as plt
    plt.rcParams['font.size']=14
    #Using matplotlib backend: Qt5Agg
    
    
    class SnaptoCursor(object):
        """
        十字カーソルを現在のカーソルのｘ値から最も近いxの点に飛ばす。
        """
    
        def __init__(self, ax, x, y):
            self.ax = ax
            self.lx = ax.axhline(color='g')  # the horiz line
            self.ly = ax.axvline(color='g')  # the vert line
            self.x = x
            self.y = y
            # location of point
    
            
        def mouse_move(self, event):
            if not event.inaxes:
                return
    
            x, y = event.xdata, event.ydata
            indx = np.argmin(np.abs(self.x-x))
            x = self.x[indx]
            y = self.y[indx]
            # update the line positions
            self.lx.set_ydata(y)
            self.ly.set_xdata(x)
            #update title
            self.ax.set_title('x=%1.2f, y=%1.2f' % (x, y))
            self.ax.figure.canvas.draw()
    
    
    fig,ax = plt.subplots(figsize=(8, 6))
    x, y = np.random.rand(2,20)
    [ax.plot(x[i], y[i], 'o',mew=2,mec='k', ms=20) for i in range(len(x))]
    snap_cursor = SnaptoCursor(ax, x, y)
    fig.canvas.mpl_connect('motion_notify_event', snap_cursor.mouse_move)
     
        
    import matplotlib
    print(matplotlib.__version__)
    3.2.0
    
    print(np.__version__)
    1.18.1
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

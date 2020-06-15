---
title: camera
date: 2020-05-07
---
Example Python program camera.py
For Python version 2.x.
To test your Python version use:

    python --version

## Modules

* import numpy as np
* import cv2
* import time
* import matplotlib.animation as animation
* import matplotlib.pyplot as plt
* import matplotlib.cm as cm
* try: import Tkinter as Tk
* except ImportError: import tkinter as Tk
* from matplotlib.backends.backend_tkagg import FigureCanvasTkAgg, NavigationToolbar2TkAgg
* from matplotlib.figure import Figure

## Classes

* class Camera:

## Methods

* def __init__(self,channel=0):
* def acquire(self):
* def close(self):
* def updatefig(*args):

## Code

Python tkinter example

    # Display webcam image, plus plasma diagnostics
    # version 2, 2013-09-25
    # Amar
    # Changelog:
    #       v2: Very slight modification of http://matplotlib.org/examples/animation/dynamic_image.html
    
    import numpy as np
    import cv2
    import time
    import matplotlib.animation as animation
    import matplotlib.pyplot as plt
    import matplotlib.cm as cm
    
    try: import Tkinter as Tk
    except ImportError: import tkinter as Tk
    from matplotlib.backends.backend_tkagg import FigureCanvasTkAgg, NavigationToolbar2TkAgg
    from matplotlib.figure import Figure
    
    class Camera:
        def __init__(self,channel=0):
            self.capture = cv2.VideoCapture(channel)
            self.success,self.image = self.capture.read()
            print "Beginning acquisition ...",
    
        def acquire(self):
            self.success,self.image = self.capture.read()
    
        def close(self):
            if self.capture.isOpened(): self.capture.release()
            print "released camera"
    
    camera = Camera()
    fig = plt.figure()
    fig.canvas.set_window_title('USB Camera') 
    im = plt.imshow(camera.image[:,:,0])
    
    def updatefig(*args):
        camera.acquire()
        im.set_array(camera.image[:,:,0])
        return im,
    
    ani = animation.FuncAnimation(fig, updatefig, interval=80, blit=True)
    plt.show()
    camera.close()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

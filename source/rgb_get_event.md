---
title: rgb_get_event
date: 2020-05-07
---
Example Python program rgb_get_event.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import numpy as np
* import matplotlib.pyplot as plt
* from ipywidgets import Output
* import matplotlib.ticker as ticker
* import matplotlib
* import ipywidgets

## Methods

* def onclick(event):
* def onclick(event):

## Code

Python example

    %matplotlib widget
    import numpy as np
    import matplotlib.pyplot as plt
    from ipywidgets import Output
    import matplotlib.ticker as ticker
    
    #make data
    img = np.rint(np.random.rand(5,5,3) * 255).astype(int)
    
    fig, ax = plt.subplots(figsize=(4,4))
    im = ax.imshow(img, interpolation='nearest',origin='lower',alpha=1)
    
    out = Output()
    display(out)
    @out.capture(clear_output=True)
    
    def onclick(event):
        px, py = event.xdata, event.ydata
        px = int(np.rint(px))
        py = int(np.rint(py))
        rgb = img[py,px]    
        ax.plot(px,py,'wo')
        ax.set_title('R=%d, G=%d, B=%d' %(rgb[0],rgb[1],rgb[2]))
        print('R=%d, G=%d, B=%d' %(rgb[0],rgb[1],rgb[2]))
        
    cid = fig.canvas.mpl_connect('button_press_event', onclick)
    
    #load image form https://www.irasutoya.com/2019/10/blog-post_187.html
    img = plt.imread('plant_saboten5.png')
    
    fig, ax = plt.subplots(figsize=(4,4))
    im = ax.imshow(img)
    ax.xaxis.set_major_locator(ticker.NullLocator())
    ax.yaxis.set_major_locator(ticker.NullLocator())
    
    def onclick(event):
        px, py = event.xdata, event.ydata
        px = int(np.rint(px))
        py = int(np.rint(py))
        rgba = img[py,px]    
        ax.set_title('R=%.3f, G=%.3f,\n B=%.3f, a=%.3f' %(rgba[0],rgba[1],rgba[2],rgba[3]))
        fig.set_facecolor((rgba[0],rgba[1],rgba[2],rgba[3]))
    cid = fig.canvas.mpl_connect('button_press_event', onclick)
    
    #version
    import matplotlib
    print(matplotlib.__version__)
    #3.2.0
    print(np.__version__)
    #1.18.1
    import ipywidgets
    print(ipywidgets.__version__)
    #7.5.1
     

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

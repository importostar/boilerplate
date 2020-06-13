---
title: cactus_graphics
date: 2020-05-07
---
Example Python program cactus_graphics.py

## Modules

* import matplotlib.pyplot as plt
* import numpy as np
* from matplotlib.offsetbox import OffsetImage, AnnotationBbox 
* from IPython.display import HTML
* from matplotlib.animation import FuncAnimation

## Methods

* def init():
* def update(i):

## Code

Python example

    %matplotlib inline
    import matplotlib.pyplot as plt
    import numpy as np
    from matplotlib.offsetbox import OffsetImage, AnnotationBbox 
    from IPython.display import HTML
    from matplotlib.animation import FuncAnimation
    
    fig, ax = plt.subplots(figsize=(16,9)) 
    image = 'cactus7.png' 
    image = plt.imread(image) 
    im = OffsetImage(image, zoom=.3) 
    
    artists = [] 
    xdata, ydata = [0], [0]
    ln, = plt.plot(xdata, ydata, 'r', lw=9, animated=True)
    annotation = AnnotationBbox(im,(xdata[0], ydata[0]),xycoords='data', frameon=False)
    artists.append(ax.add_artist(annotation))
    
    def init():
        ax.set_xlim(-25, 25)
        ax.set_ylim(-25, 25)
        ax.set_aspect('equal')
        ax.axis('off')    
        #ax.patch.set_facecolor('gold')  # 図全体の背景色
    
    def update(i):
        x_i = 0.5 * i * np.cos(i)
        y_i = 0.5 * i * np.sin(i)
        xdata.append(x_i)
        ydata.append(y_i)
        ln.set_data(xdata, ydata)
        annotation.xybox = (x_i,y_i)
    
        return ln, annotation
    
    ani = FuncAnimation(fig, update, frames=np.linspace(0, 16*np.pi, 300),
                        interval=100,init_func=init, blit=False)
    HTML(ani.to_html5_video())
    #dpi=100
    #ani.save('rasen.mp4', writer="ffmpeg",dpi=dpi)
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

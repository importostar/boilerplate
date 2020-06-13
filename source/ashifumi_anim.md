---
title: ashifumi_anim
date: 2020-05-07
---
Example Python program ashifumi_anim.py

## Modules

* import numpy as np
* import matplotlib.pyplot as plt
* import matplotlib.patches as patches
* import matplotlib.animation as animation
* from IPython.display import HTML

## Methods

* def update(num):

## Code

Python example

    %matplotlib inline
    import numpy as np
    import matplotlib.pyplot as plt
    import matplotlib.patches as patches
    import matplotlib.animation as animation
    from IPython.display import HTML
    fig,ax = plt.subplots(ncols=2,figsize=(12,6))
    
    [ax[0].axhspan(0.05*i, 0.025+0.05*i,xmin=0, xmax=1, facecolor='0',zorder=1) for i in range(21)]
    [ax[0].axhspan(0.05*i-0.025, 0.05*i,xmin=0, xmax=1, facecolor='0.8',zorder=1) for i in range(21)]
    
    rect_1 = patches.Rectangle(xy = (0.2, 0), width = 0.1,height = .1, fc = "0",zorder =2)
    ax[0].add_patch(rect_1)
    rect_2 = patches.Rectangle(xy = (0.45, 0), width = 0.1,height = .1, fc = "lime",zorder =2)
    ax[0].add_patch(rect_2)
    rect_3 = patches.Rectangle(xy = (0.7, 0), width = 0.1,height = .1, fc = "0.8",zorder =2)
    ax[0].add_patch(rect_3)
    
    rect_4 = patches.Rectangle(xy = (0.2, 0), width = 0.1,height = .1, fc = "0",zorder =2)
    ax[1].add_patch(rect_4)
    rect_5 = patches.Rectangle(xy = (0.45, 0), width = 0.1,height = .1, fc = "lime",zorder =2)
    ax[1].add_patch(rect_5)
    rect_6 = patches.Rectangle(xy = (0.7, 0), width = 0.1,height = .1, fc = "0.8",zorder =2)
    ax[1].add_patch(rect_6)
    
    
    ax[0].set_ylim(-0.,1.0)
    ax[0].set_xlim(-0.,1.0)
    ax[1].set_ylim(-0.,1.0)
    ax[1].set_xlim(-0.,1.0)
    ax[0].axis('off')
    ax[1].axis('off')
    
    def update(num):
        rect_1.set_height(.1+.005*num)
        rect_2.set_height(.1+.005*num)
        rect_3.set_height(.1+.005*num)
        rect_4.set_height(.1+.005*num)
        rect_5.set_height(.1+.005*num)
        rect_6.set_height(.1+.005*num)
        
        return fig,
    
            
    ani = animation.FuncAnimation(fig, update, 100, blit=True, interval=50)
    HTML(ani.to_html5_video())
    #ani.save('ashifumi_anim.mp4', writer="ffmpeg",dpi=100)
    
     

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

---
title: munker_anim
date: 2020-05-07
---
Example Python program munker_anim.py

## Modules

* import matplotlib.pyplot as plt
* import matplotlib.patches as patches
* import matplotlib.animation as animation
* from IPython.display import HTML

## Methods

* def update(num):

## Code

Python example

    %matplotlib inline
    import matplotlib.pyplot as plt
    import matplotlib.patches as patches
    import matplotlib.animation as animation
    from IPython.display import HTML
    
    fig,ax = plt.subplots(figsize=(8,8))
    
    def update(num):
        ax.cla()
        ax.set_ylim(-0.,1.0)
        ax.set_xlim(-0.,1.0)
        #left side  white -> lime -> black
        [ax.axhspan(0.8/(2*(num+1))*i, 0.4/(2*(num+1))+0.8/(2*(num+1))*i,xmin=0, xmax=.5, facecolor='0',zorder=2) for i in range(3*(num+1))]
        cp6_l = patches.CirclePolygon(xy = (0.25, 0.475), radius = 0.2,
                                      resolution = 6, fc = "lime",zorder =1)
        ax.add_patch(cp6_l)
        
        #right side black -> lime -> white
        [ax.axhspan(0.8/(2*(num+1))*i, 0.4/(2*(num+1))+0.8/(2*(num+1))*i,xmin=0.5, xmax=1, facecolor='0',zorder=1) for i in range(3*(num+1))]
        [ax.axhspan(0.8/(2*(num+1))*i-0.4/(2*(num+1)), 0.8/(2*(num+1))*i,xmin=0.5, xmax=1, facecolor='1',zorder=3) for i in range(3*(num+1))]
        cp6_r = patches.CirclePolygon(xy = (0.75, 0.475), radius = 0.2,
        resolution = 6, fc = "lime",zorder =2)
        ax.add_patch(cp6_r)
        
        ax.axis("off")
    
        return fig,
    
            
    ani = animation.FuncAnimation(fig, update, 20, blit=True, interval=150)
    HTML(ani.to_html5_video())
    #ani.save('munker_anim.mp4', writer="ffmpeg",dpi=100)
    
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

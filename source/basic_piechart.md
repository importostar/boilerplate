---
title: basic_piechart
date: 2020-05-07
---
Example Python program basic_piechart.py

## Modules

* import matplotlib.pyplot as plt
* import numpy as np
* import matplotlib.pyplot as plt
* import matplotlib.animation as animation
* from IPython.display import HTML
* import numpy as np
* import matplotlib.pyplot as plt
* import matplotlib.animation as animation
* from IPython.display import HTML

## Methods

* def update(num,chocopie, a,b):
* def update(num,chocopie, a,b):

## Code

Python example

    %matplotlib inline
    import matplotlib.pyplot as plt
    
    # Pie chart, where the slices will be ordered and plotted counter-clockwise:
    labels = 'Blackthunder', 'Tirolchoco', 'Mugichoco', 'Chocoflake'
    sizes = [15, 30, 45, 10]
    explode = (0, 0, 0.1, 0)  # only "explode" the 2nd slice (i.e. 'Mugichoco')
    
    fig, ax = plt.subplots()
    ax.pie(sizes, explode=explode, labels=labels, autopct='%1.1f%%',
            shadow=True, startangle=90)
    #ax.axis('equal')  # Equal aspect ratio ensures that pie is drawn as a circle.
    #fig.savefig("chocopie.png", dpi=150,transparent = False, bbox_inches = 'tight')
    plt.show()
    
    
    #rotate anim
    import numpy as np
    import matplotlib.pyplot as plt
    import matplotlib.animation as animation
    from IPython.display import HTML
    
    labels = 'Blackthunder', 'Tirolchoco', 'Mugichoco', 'Chocoflake'
    sizes = [15, 30, 45, 10]
    explode = (0, 0, 0.1, 0)  # only "explode" the 2nd slice (i.e. 'Mugichoco')
    
    def update(num,chocopie, a,b):
        if len(chocopie) > 0:
            ax.cla()
        
        chocopie,a,b, = ax.pie(sizes, explode=explode, labels=labels, autopct='%1.1f%%',
        shadow=True, startangle=4*num)
        
        ax.set_title("startangle = "+str(4 * num)[:4])
    
    fig, ax = plt.subplots()    
    chocopie,a,b, = ax.pie(sizes, explode=explode, labels=labels, autopct='%1.1f%%',shadow=True, startangle=0)
    ani = animation.FuncAnimation(fig, update, frames=91,fargs=[chocopie, a,b], interval=100)
    HTML(ani.to_html5_video())
    #dpi=100
    #ani.save('rotate_pie.mp4', writer="ffmpeg",dpi=dpi)
    
    
    #explode anim
    
    import numpy as np
    import matplotlib.pyplot as plt
    import matplotlib.animation as animation
    from IPython.display import HTML
    
    labels = 'Blackthunder', 'Tirolchoco', 'Mugichoco', 'Chocoflake'
    sizes = [15, 30, 45, 10]
    explode = (0, 0, 0, 0)  
    def update(num,chocopie, a,b):
        if len(chocopie) > 0:
            ax.cla()
        if num < 25:
            explode = (0, 0, 0.01*num, 0) 
            ax.set_title("explode = "+str(0.01*num)[:4])
        else:
            explode = (0, 0, -0.01*num+0.5, 0)
            ax.set_title("explode = "+str(-0.01*num+0.5)[:4])
    
        chocopie,a,b, = ax.pie(sizes, explode=explode, labels=labels, autopct='%1.1f%%',
                               shadow=True,startangle=90)
        
    fig, ax = plt.subplots()    
    chocopie,a,b, = ax.pie(sizes, explode=explode, labels=labels, autopct='%1.1f%%',shadow=True, startangle=0)
    ani = animation.FuncAnimation(fig, update, frames=51,fargs=[chocopie, a,b], interval=100)
    HTML(ani.to_html5_video())
    #dpi=100
    #ani.save('explode_pie.mp4', writer="ffmpeg",dpi=dpi)
    
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

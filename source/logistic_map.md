---
title: logistic_map
date: 2020-05-07
---
Example Python program logistic_map.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import matplotlib.pyplot as plt
* import matplotlib as mpl
* from matplotlib import animation
* from matplotlib.animation import PillowWriter
* import numpy as np
* import seaborn as sn

## Methods

* def logistic_map(z=0.2, r=2):

## Code

Python example

    import matplotlib.pyplot as plt
    import matplotlib as mpl
    from matplotlib import animation
    from matplotlib.animation import PillowWriter
    import numpy as np
    import seaborn as sn
    
    mpl.use("TkAgg")
    plt.style.use('seaborn')
    mpl.rcParams['figure.dpi'] = 200
    
    def logistic_map(z=0.2, r=2):
        res = []
        for _ in range(20):
            z = r * z * (1 - z)
            res.append(z)
        return res
    
    
    
    if __name__ == "__main__":
        fig = plt.figure()
    
        fig.tight_layout(rect=[0, 0.03, 1, 0.95])
        fig.show()
        fig.canvas.draw()
        ims = []
        z = []
        plt.ylabel("x")
        plt.xlabel("r")
        for j, i in enumerate(np.linspace(2, 4, 500)):
            z.append(logistic_map(z=0.2, r=i))
            f = plt.plot(np.linspace(2.6, 4, len(z)), z, "k.", markersize=3,
                         alpha=1)
    
            print(i)
            ims.append(f)
    
            #fig.canvas.draw()
    
        ani = animation.ArtistAnimation(fig, ims, interval=3, 
                                  repeat_delay=500)
    
        writer = PillowWriter(fps=len(ims))
        ani.save("logistic.gif", writer=writer)
    
        fig.tight_layout(rect=[0, 0.03, 1, 0.95])
        plt.show()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

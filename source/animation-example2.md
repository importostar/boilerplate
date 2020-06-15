---
title: animation example2
date: 2020-05-07
---
Example Python program animation-example2.py
For Python version 2.x.
To test your Python version use:

    python --version

## Modules

* import numpy as np
* import matplotlib.pyplot as plt
* import matplotlib.animation as mplanim

## Methods

* def init():
* def update(frame, ax, lines):
* def _main():

## Code

Python example

    # fast plot
    
    import numpy as np
    import matplotlib.pyplot as plt
    import matplotlib.animation as mplanim
    
    
    def init():
        print "init"
    
    
    def update(frame, ax, lines):
        x = np.arange(0, 1, 0.01)
        y = np.sin(5 * x + frame)
    
        lines[0].set_xdata(x)
        lines[0].set_ydata(y)
    
    
    def _main():
        fig = plt.figure()
        ax = fig.add_subplot(111)
        lines = ax.plot([], [], marker='+')  # empty lines
        ax.set_xlim([0, 1])
        ax.set_ylim([-1, 1])
    
        fps = 60
        frames = np.arange(0, 100, 0.1)
        anim = mplanim.FuncAnimation(
            fig,
            func=update,
            frames=frames,
            init_func=init,
            interval=1000. / fps,  # msec
            fargs=[ax, lines],
            save_count=len(frames),
        )
    
        # anim.save('test.mp4', fps=fps)
        plt.show()
    
    
    if __name__ == '__main__':
        _main()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

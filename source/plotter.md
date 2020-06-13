---
title: plotter
date: 2020-05-07
---
Example Python program plotter.py

## Modules

* import datetime as dt
* import random
* import matplotlib as mpl
* import matplotlib.animation as animation
* import matplotlib.pyplot as plt

## Classes

* class Plotter:

## Methods

* def __init__(self, interval: int, limit: int):
* def __render_frame(self, i: int):
* def start(self):

## Code

Python example

    import datetime as dt
    import random
    
    import matplotlib as mpl
    import matplotlib.animation as animation
    import matplotlib.pyplot as plt
    
    # disables default toolbar. 
    # comment out this line if you wanna show them.
    mpl.rcParams['toolbar'] = 'None'
    
    
    class Plotter:
        def __init__(self, interval: int, limit: int):
            self.interval = interval
            self.limit = limit
    
            # init data points
            self.timestamps = []
            self.values = []
    
            # init plot figure
            self.fig, self.ax = plt.subplots()
    
        def __render_frame(self, i: int):
            val = random.uniform(0, 1)
    
            self.timestamps.append(dt.datetime.now())
            self.values.append(val)
    
            # truncate to self.limit data points
            self.timestamps = self.timestamps[-self.limit:]
            self.values = self.values[-self.limit:]
    
            # redraw plot
            self.ax.clear()
            self.ax.grid(True)
            self.ax.plot_date(self.timestamps, self.values, 'b-')
    
        def start(self):
            # periodically update the graph
            a = animation.FuncAnimation(
                fig=self.fig,
                func=self.__render_frame,
                interval=self.interval,
            )
    
            plt.show()
    
    
    plotter = Plotter(interval=500, limit=1000)
    plotter.start()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

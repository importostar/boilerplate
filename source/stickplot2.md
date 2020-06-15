---
title: stickplot2
date: 2020-05-07
---
Example Python program stickplot2.py

## Modules

* import matplotlib as mpl
* import matplotlib.pyplot as plt
* import numpy as np
* import datetime

## Methods

* def stick(axes, times, speeds, directions, units=''):

## Code

Python example

    """
    some code to do a stick plot with MPL
    
    This version uses matplotlib's quiver.
    
    Credits
    -------
    Chris Barker
    http://matplotlib.1069221.n5.nabble.com/Stick-Plot-td21479.html
    
    See also
    --------
    http://matplotlib.1069221.n5.nabble.com/scaling-arrows-in-quiver-td23758.html
    """
    
    import matplotlib as mpl
    import matplotlib.pyplot as plt
    import numpy as np
    
    import datetime
    
    
    def stick(axes, times, speeds, directions, units=''):
        """
        Create a stick plot of the given data on the given axes.
       
        Stick plots are commonly used to display time series of
        a vector quantity at a point, such as wind or ocean current observations.
        
        Call signature::
            stick(axes, times, speed, direction, units='m/s')
       
        Arguments: 
           *axes*:  The axes object you want to plot on
           *times*: An array of datetime objects giving the time of the
                    observations
           *speeds*: An array of the velocities of the observations
           *directions*: An array of the directions of the observations (in
                         degrees from North, where North is up on the plot)
           *units*:  A string with the units of the observation
        
        """
    
        props = {'units' : "dots",
                 'width' : 2,
                 'headwidth': 0,
                 'headlength': 0,
                 'headaxislength': 0,
                 'scale' : .1,
                 }
    
        ##fixme: this should use some smarts to fit the data...
        label_scale = 10
        unit_label = "%3g %s"%(label_scale, units)
    
        y = np.zeros_like(speeds)
        dir_rad = directions / 180. * np.pi
        u = np.sin(dir_rad) * speeds
        v = np.cos(dir_rad) * speeds
    
        Q = ax.quiver(times, y, u, v, **props)
        ax.quiverkey(Q, X=0.1, Y=0.95, U=label_scale, label=unit_label, coordinates='axes', labelpos='S')
        yaxis = ax.yaxis
        yaxis.set_ticklabels([])
    
    if __name__ == '__main__':
    
        ## some sample data:
    
        data = np.array([(10,  0.5),
                         (10,  22.5),
                         (10, 45.0),
                         (10, 67.5),
                         (10, 90.0),
                         (10, 112.5),
                         (10, 135.0),
                         (10, 157.5),
                         (10, 180.0),
                         (10, 202.5),
                         (10, 225.0),
                         (10, 247.5),
                         (10, 270.0),
                         (10, 292.5),
                         (10, 315.0),
                         (10, 337.5),
                         ( 8, 157.5),
                         (12, 180.0),
                         (15, 202.5),
                         ( 7, 225.0),
                         ( 5, 247.5),
                         (16, 270.0),
                         (20, 292.5),
                         (22, 315.0),
                         (15, 337.5),
                         (12,  22.5),
                         (17, 25.0),
                         (18, 30),
                         ], dtype=np.float)
        data = np.r_[data, data, data, data, data, data]
        speeds  = data[:,0]
        directions  = data[:,1]
        times = range(len(speeds))
        #times = [datetime.datetime(2009, 5, 13, 0) + datetime.timedelta(hours=h) for h in times]
    
        fig = plt.figure(1)
        fig.clear()
    
        ax = fig.add_subplot(1,1,1)
        stick(ax, times, speeds, directions, units='knots')
    
        plt.draw()
        plt.show()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

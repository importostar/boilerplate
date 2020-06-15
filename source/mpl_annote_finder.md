---
title: mpl_annote_finder
date: 2020-05-07
---
Example Python program mpl_annote_finder.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import math
* import matplotlib.pyplot as plt

## Classes

* class AnnoteFinder(object):

## Methods

* def __init__(self, xdata, ydata, annotes, ax=None, xtol=None, ytol=None):
* def distance(self, x1, x2, y1, y2):
* def __call__(self, event):
* def drawAnnote(self, ax, x, y, annote):
* def drawSpecificAnnote(self, annote):

## Code

Python example

    
    '''
    This is an update for the recipes found on this website:
    http://scipy-cookbook.readthedocs.org/items/Matplotlib_Interactive_Plotting.html
    
    It was discussed and solved as issue number 5601 on the following site:
    https://github.com/matplotlib/matplotlib/issues
    
    Now it will works correctly also on python 3
    Can you please push this update scipy-cookbook to the website?
    '''
    
    import math
    
    import matplotlib.pyplot as plt
    
    
    class AnnoteFinder(object):
        """callback for matplotlib to display an annotation when points are
        clicked on.  The point which is closest to the click and within
        xtol and ytol is identified.
    
        Register this function like this:
    
        scatter(xdata, ydata)
        af = AnnoteFinder(xdata, ydata, annotes)
        connect('button_press_event', af)
    
        """
    
        def __init__(self, xdata, ydata, annotes, ax=None, xtol=None, ytol=None):
            self.data = list(zip(xdata, ydata, annotes))
            if xtol is None:
                xtol = ((max(xdata) - min(xdata))/float(len(xdata)))/2
            if ytol is None:
                ytol = ((max(ydata) - min(ydata))/float(len(ydata)))/2
            self.xtol = xtol
            self.ytol = ytol
            if ax is None:
                self.ax = plt.gca()
            else:
                self.ax = ax
            self.drawnAnnotations = {}
            self.links = []
    
        def distance(self, x1, x2, y1, y2):
            """
            return the distance between two points
            """
            return(math.sqrt((x1 - x2)**2 + (y1 - y2)**2))
    
        def __call__(self, event):
    
            if event.inaxes:
    
                clickX = event.xdata
                clickY = event.ydata
                if (self.ax is None) or (self.ax is event.inaxes):
                    annotes = []
                    # print(event.xdata, event.ydata)
                    for x, y, a in self.data:
                        # print(x, y, a)
                        if ((clickX-self.xtol < x < clickX+self.xtol) and
                                (clickY-self.ytol < y < clickY+self.ytol)):
                            annotes.append(
                                (self.distance(x, clickX, y, clickY), x, y, a))
                    if annotes:
                        annotes.sort()
                        distance, x, y, annote = annotes[0]
                        self.drawAnnote(event.inaxes, x, y, annote)
                        for l in self.links:
                            l.drawSpecificAnnote(annote)
    
        def drawAnnote(self, ax, x, y, annote):
            """
            Draw the annotation on the plot
            """
            if (x, y) in self.drawnAnnotations:
                markers = self.drawnAnnotations[(x, y)]
                for m in markers:
                    m.set_visible(not m.get_visible())
                self.ax.figure.canvas.draw_idle()
            else:
                t = ax.text(x, y, " - %s" % (annote),)
                m = ax.scatter([x], [y], marker='d', c='r', zorder=100)
                self.drawnAnnotations[(x, y)] = (t, m)
                self.ax.figure.canvas.draw_idle()
    
        def drawSpecificAnnote(self, annote):
            annotesToDraw = [(x, y, a) for x, y, a in self.data if a == annote]
            for x, y, a in annotesToDraw:
                self.drawAnnote(self.ax, x, y, a)
    
    if __name__ == '__main__':
        x = range(10)
        y = range(10)
        annotes = ['a', 'b', 'c', 'd', 'e', 'f', 'g', 'h', 'i', 'j']
        fig, ax = plt.subplots()
        ax.scatter(x, y)  # or ax.plot(x,y,'bo')
        af = AnnoteFinder(x, y, annotes, ax=ax)
        fig.canvas.mpl_connect('button_press_event', af)
    
        plt.show()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

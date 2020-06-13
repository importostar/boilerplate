---
title: wxpython_with_matplotlib
date: 2020-05-07
---
Example Python program wxpython_with_matplotlib.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import matplotlib
* import wx
* from matplotlib.backends.backend_wxagg import FigureCanvasWxAgg
* from matplotlib.figure import Figure
* import numpy as np

## Classes

* class myWxPlot(wx.Panel):

## Methods

* def __init__(self, parent):
* def update_graph(self, event):
* def draw(self, event=None):
* def main():

## Code

Python example

    # -*- coding: utf-8 -*-
    
    import matplotlib
    matplotlib.interactive(True)
    matplotlib.use('WXAgg')
    
    import wx
    
    from matplotlib.backends.backend_wxagg import FigureCanvasWxAgg
    from matplotlib.figure import Figure
    import numpy as np
    
    class myWxPlot(wx.Panel):
        def __init__(self, parent):
            self.parent = parent
            wx.Panel.__init__(self, parent)
            
            self.lastplot = None
    
            #matplotlib figure
            self.figure = Figure(None)
            self.figure.set_facecolor((0.9, 0.9, 1.))
            self.subplot = self.figure.add_subplot(111)
            #canvas
            self.canvas = FigureCanvasWxAgg(self, -1, self.figure)
            self.canvas.SetBackgroundColour(wx.Colour(100,255,255))
    
            sizer = wx.BoxSizer(wx.VERTICAL)
            sizer.Add(self.canvas, 1, wx.EXPAND)
            self.SetSizer(sizer)
            self.draw()
            
            self.timer = wx.Timer(self, 1)
            self.Bind(wx.EVT_TIMER, self.update_graph, self.timer)
            self.timer.Start(1000)
    
        def update_graph(self, event):
            print('Uppdate graph!')
            self.draw(event)
    
        def draw(self, event=None):
            print('draw!')
            
            if self.lastplot:
                self.lastplot[0].remove()
            
            x = np.random.rand(100) * 100
            # x = np.arange(-10, 10, 0.01)
            y = np.cos(x)
            self.lastplot = self.subplot.plot(x, y)
            self.subplot.set_title('sample (cos)')
            self.subplot.set_xlabel('x')
            self.subplot.set_ylabel('y')
            # self.Refresh()  # 単体だと効果なし
            # self.Update()  # 単体で効果なし
            self.canvas.draw()  # 単体で有効！
    
    
    def main():
        app = wx.App()
        frame = wx.Frame(None, size=(500,500))
        panel = myWxPlot(frame)
        frame.Show()
        app.MainLoop()
    
    if __name__ == '__main__':
        main()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

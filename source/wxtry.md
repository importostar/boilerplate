---
title: wxtry
date: 2020-05-07
---
Example Python program wxtry.py
For Python version 2.x.
To test your Python version use:

    python --version

## Modules

* import numpy as np
* import wx
* import matplotlib
* from matplotlib.backends.backend_wxagg import FigureCanvasWxAgg
* from matplotlib.backends.backend_wxagg import NavigationToolbar2WxAgg as NavigationToolbar
* from matplotlib.figure import Figure
* from matplotlib.pyplot import gcf, setp

## Classes

* class FourierDemoFrame(wx.Frame):
* class FourierDemoWindow(wx.Window):
* class App(wx.App):

## Methods

* def __init__(self, *args, **kwargs):
* def __init__(self, *args, **kwargs):
* def draw(self):
* def OnLeftDown(self, event):
* def OnInit(self):

## Code

Python example

    #!/usr/bin/env python
    
    """
    wxPython to append to a list 'a' the x position clicked with the mouse. 
    """
    
    import numpy as np
    import wx
    import matplotlib
    matplotlib.interactive(False)
    matplotlib.use('WXAgg')
    from matplotlib.backends.backend_wxagg import FigureCanvasWxAgg
    from matplotlib.backends.backend_wxagg import NavigationToolbar2WxAgg as NavigationToolbar
    from matplotlib.figure import Figure
    from matplotlib.pyplot import gcf, setp
    
    
    class FourierDemoFrame(wx.Frame):
        def __init__(self, *args, **kwargs):
            wx.Frame.__init__(self, *args, **kwargs)
            self.fourierDemoWindow = FourierDemoWindow(self)
    
    class FourierDemoWindow(wx.Window):
        def __init__(self, *args, **kwargs):
            wx.Window.__init__(self, *args, **kwargs)
            self.figure = Figure()
            self.canvas = FigureCanvasWxAgg(self, -1, self.figure)
            self.draw()
    
    
        def draw(self):
            if not hasattr(self, 'subplot1'):
                t = np.arange(0.0, 2.0, 0.01)
                s = np.sin(2*np.pi*t)
                self.subplot1 = self.figure.add_subplot(111)
                self.subplot1.plot(t,s)
                self.a=[]
                # hook some mouse events
                self.canvas.callbacks.connect('button_press_event', self.OnLeftDown)
    
        def OnLeftDown(self, event):
            valuex = (event.xdata  );valuey = (event.ydata)
            self.a.append(event.xdata)
            print self.a
            #print 'ra and dec', event.xdata, event.ydata
     
     
    class App(wx.App):
        def OnInit(self):
            self.frame1 = FourierDemoFrame(parent=None, title="Vaina", size=(900, 900))  #640, 480
            self.frame1.Show()
            return True
    
    app = App()
    app.MainLoop()      
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

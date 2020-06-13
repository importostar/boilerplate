---
title: wxpython serialdata matplotlib
date: 2020-05-07
---
Example Python program wxpython-serialdata-matplotlib.py
For Python version 2.x.
To test your Python version use:

    python --version

## Modules

* import wx
* import serial
* import matplotlib
* from matplotlib.backends.backend_wxagg import FigureCanvasWxAgg as FigureCanvas
* from matplotlib.backends.backend_wx import NavigationToolbar2Wx
* from matplotlib.figure import Figure

## Classes

* class MyFrame(wx.Frame):

## Methods

* def __init__(self, parent, title):
* def OnPaint(self, event=None):

## Code

Python example

    #!/usr/local/bin/python
    # -*- coding: utf-8 -*-
    
    import wx
    import serial
    
    # Import matplotlib for wxPython
    import matplotlib
    matplotlib.use('WXAgg')
    
    from matplotlib.backends.backend_wxagg import FigureCanvasWxAgg as FigureCanvas
    from matplotlib.backends.backend_wx import NavigationToolbar2Wx
    from matplotlib.figure import Figure
    
    
    class MyFrame(wx.Frame):
        def __init__(self, parent, title):
            super(MyFrame, self).__init__(parent, title=title,
                size=(350, 250))
    
            # Initialize the Matplotlib graph
            self.figure = Figure()
            self.axes = self.figure.add_subplot(111)
            self.canvas = FigureCanvas(self, -1, self.figure)
    
            # Create a timer for redrawing the frame every 100 milliseconds
            self.Timer = wx.Timer(self)
            self.Timer.Start(100)
            self.Bind(wx.EVT_TIMER, self.OnPaint)
    
            # Show the frame
            self.Centre()
            self.Show()
    
    
        def OnPaint(self, event=None):
            # Get data from serial port
            value = arduino.readline()
    
            # Draw the serial data
    
            # Cleare the previos graph
            self.axes.clear()
    
            # Set the Y axis limit in order to provide consistency in the visualization
            self.axes.set_ylim([0,100])
    
            # Draw the bar
            self.axes.bar(1,value)
    
            # Update the graph
            self.canvas.draw()
    
    
    # Main program
    if __name__ == '__main__':
        # Connect to serial port first
        try:
            arduino = serial.Serial('/dev/tty.usbmodem1421', 9600)
        except:
            print "Failed to connect"
            exit()
     
        # Create and launch the wx interface
        app = wx.App()
        MyFrame(None, 'Serial data test')
        app.MainLoop()
     
        # Close the serial connection
        arduino.close()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

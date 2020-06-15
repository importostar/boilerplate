---
title: opencv wx
date: 2020-05-07
---
Example Python program opencv-wx.py

## Modules

* import wx
* from wx.lib import statbmp
* import cv2
* import numpy as np
* import os
* import traceback

## Classes

* class ShowCapture(wx.Frame):

## Methods

* def __init__(self, capture, fps=10):
* def NextFrame(self, event):

## Code

Python example

    import wx
    from wx.lib import statbmp
    import cv2
    import numpy as np
    import os
    import traceback
    
    class ShowCapture(wx.Frame):
        def __init__(self, capture, fps=10):
            wx.Frame.__init__(self, None, -1, "Title")
            panel = wx.Panel(self, -1)
    
            #create a grid sizer with 5 pix between each cell
            sizer = wx.GridBagSizer(5, 5)
    
            self.capture = capture
            ret, frame = self.capture.read()
    
            height, width = frame.shape[:2]
            self.orig_height = height
            self.orig_width = width
    
            frame = cv2.cvtColor(frame, cv2.COLOR_BGR2RGB)
    
            self.bmp = wx.Bitmap.FromBuffer(width, height, frame)
            
            #create image display widgets
            self.ImgControl = statbmp.GenStaticBitmap(panel, wx.ID_ANY, self.bmp)
            
            #add image widgets to the sizer grid
            sizer.Add(self.ImgControl, (3, 0), (1,4), wx.EXPAND, 5)
            
            #set the sizer and tell the Frame about the best size
            panel.SetSizer(sizer)
            sizer.SetSizeHints(self)
            panel.Layout()
            panel.SetFocus()
    
            #start a timer that's handler grabs a new frame and updates the image widgets
            self.timer = wx.Timer(self)
            self.fps = fps
            self.timer.Start(1000./self.fps)
    
            #bind timer events to the handler
            self.Bind(wx.EVT_TIMER, self.NextFrame)
    
        def NextFrame(self, event):
            ret, self.orig_frame = self.capture.read()
            if ret:
                frame = cv2.cvtColor(self.orig_frame, cv2.COLOR_BGR2RGB)
    
                self.bmp.CopyFromBuffer(frame)
                self.ImgControl.SetBitmap(self.bmp)
    
    if __name__ == "__main__":
        capture = cv2.VideoCapture(0)
        #capture.set(cv.CV_CAP_PROP_FRAME_WIDTH, 320)
        #capture.set(cv.CV_CAP_PROP_FRAME_HEIGHT, 240)
    
        app = wx.App()
        frame = ShowCapture( capture)
        frame.Show()
        app.MainLoop()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

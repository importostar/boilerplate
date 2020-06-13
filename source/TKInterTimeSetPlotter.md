---
title: TKInterTimeSetPlotter
date: 2020-05-07
---
Example Python program TKInterTimeSetPlotter.py

## Modules

* import matplotlib
* import matplotlib.pyplot as plt
* from PIL import Image, ImageTk
* from tkinter import Tk, Label, Frame  # Python 3
* # from Tkinter import Tk, Label, Frame  # Python 2
* import io

## Classes

* class TimeSetPlotter(Frame):

## Methods

* def __init__(self, timeset, master):
* def update_image(self):

## Code

Python tkinter example

    import matplotlib
    matplotlib.use("Agg")
    import matplotlib.pyplot as plt
    
    from PIL import Image, ImageTk
    from tkinter import Tk, Label, Frame  # Python 3
    # from Tkinter import Tk, Label, Frame  # Python 2
    
    #############################################################
    #  Please note that the previous examples were in Python 2  #
    #############################################################
    
    import io
    
    class TimeSetPlotter(Frame):
        def __init__(self, timeset, master):
            Frame.__init__(self, master)
            self.pack()
            self.label = Label(self)
            self.label.pack()
            
            self.timeset = timeset
            
            self.figure = plt.figure()
            plt.ylim((0,60))
            self.graph = self.figure.add_subplot(111)
            
            self.graph.plot([x.second for x in self.timeset.set])
            
            self.buffer_ = io.BytesIO()
            self.figure.savefig(self.buffer_, format="png")
            self.buffer_.seek(0)  # After saving to a buffer, you need to seek back to the "front"
            self.img = Image.open(self.buffer_)
            self.photo = ImageTk.PhotoImage(self.img)  # This is how we translate a PIL image into something tkinter-friendly
            self.label.config(image=self.photo)  # use "config" to set properties of tkinter widgets
            
            self.after(500, self.update_image)  # setting our super-sexy callback function for 500 ms
            
        def update_image(self):
            self.graph.clear()  # matplotlib will just keep piling on the plots unless you call this
            self.graph.plot([x.second for x in self.timeset.set])
            plt.ylim((0,60))  # set the y-axis limits after you call "plot"
            
            self.buffer_.seek(0)
            self.figure.savefig(self.buffer_, format="png")
            self.buffer_.seek(0)
            self.img = Image.open(self.buffer_)
            self.photo = ImageTk.PhotoImage(self.img)
            self.label.config(image=self.photo)
            
            self.after(50, self.update_image)  # make sure this function keeps on running

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

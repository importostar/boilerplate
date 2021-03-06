---
title: fast tk
date: 2020-05-07
---
Example Python program fast-tk.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import tkinter
* from PIL import Image, ImageTk
* import time
* import fastpic

## Classes

* class GeneratedPngDisplay(object):

## Methods

* def __init__(self):
* def update_image(self):
* def main():

## Code

Python tkinter example

    # use a Tkinter label as a panel/frame with a background image
    # note that Tkinter only reads gif and ppm images
    # use the Python Image Library (PIL) for other image formats
    # free from [url]http://www.pythonware.com/products/pil/index.htm[/url]
    # give Tkinter a namespace to avoid conflicts with PIL
    # (they both have a class named Image)
    
    import tkinter
    from PIL import Image, ImageTk
    import time
    import fastpic
    
    class GeneratedPngDisplay(object):
        def __init__(self):
            self.root = tkinter.Tk()
            self.root.title('Generated Image Display')
    
            # get the image size
            w = 200
            h = 200
    
            # position coordinates of root 'upper left corner'
            x = 0
            y = 0
    
            # make the root window the size of the image
            self.root.geometry("%dx%d+%d+%d" % (w, h, x, y))
    
            self.iteration = 0
            png = fastpic.generate(fastpic.RED, fastpic.BLACK)
            img = ImageTk.PhotoImage(png)
    
            # root has no image argument, so use a label as a panel
            self.panel = tkinter.Label(self.root, image=img)
            self.panel.pack(side=tkinter.TOP, fill=tkinter.BOTH, expand=tkinter.YES)
    
            self.root.after(1000, self.update_image)
            self.root.mainloop()
    
        def update_image(self):
            print("Iteration", self.iteration)
            if self.iteration % 2 == 0:
                png = fastpic.generate(fastpic.RED, fastpic.WHITE)
                img = ImageTk.PhotoImage(png)
                self.panel.configure(image=img)
                self.panel.image = img
            else:
                png = fastpic.generate(fastpic.WHITE, fastpic.BLACK)
                img = ImageTk.PhotoImage(png)
                self.panel.configure(image=img)
                self.panel.image = img
            
            self.iteration += 1
            self.root.after(1000, self.update_image)
    
    def main():
        app = GeneratedPngDisplay()
    
    if __name__ == '__main__':
        main()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

---
title: MandelbrotSet
date: 2020-05-07
---
Example Python program MandelbrotSet.py

## Modules

* from Tkinter import *
* import Tkinter

## Methods

* def iterate(x, y, iterationNum): # I am not sure if I am doing this part correctly.
* def pixel(image,x,y,r,g,b):
* def mandelbrot():

## Code

Python tkinter example

    from Tkinter import *
    import Tkinter
    def iterate(x, y, iterationNum): # I am not sure if I am doing this part correctly.
        z = 0
        coord = complex(x, y)
        while iterationNum:
            z = z * z + coord
            if z ** 2 > 4:
                return False
        return True
    
    def pixel(image,x,y,r,g,b):
       """Place pixel at pos=(x,y) on image, with color=(r,g,b)"""
       image.put("#%02x%02x%02x" % (r,g,b), (y, x))
    def mandelbrot():
        WIDTH = 640; HEIGHT = 480
        TopLeftX = -200; BottomRightX = 200
        TopLeftY = 200; BottomRightY = -200
        Increment = 5
        maxIt = 100
        w = BottomRightX - TopLeftX
        h = TopLeftY - BottomRightY
        canvas = Canvas(window, width = WIDTH, height = HEIGHT, bg = "#ffffff")
        img = PhotoImage(width = WIDTH, height = HEIGHT)
        canvas.create_image((0, 0), image = img, state = "normal", anchor = Tkinter.NW)
        for x in xrange(TopLeftX, BottomRightX, -5):
            for y in xrange(TopLeftY, BottomRightY, -5):
                xnum = x / 100.0
                ynum = y / 100.0
                if iterate(xnum, ynum, maxIt):
                    pixel(img, xnum, ynum, 255, 0, 0)
                else:
                    pixel(img, xnum, ynum, 255, 255, 255)
        canvas.pack()
        mainloop()
    
    mandelbrot()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

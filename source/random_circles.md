---
title: random_circles
date: 2020-05-07
---
Example Python program random_circles.py

## Modules

* import tkinter#Library
* import  random #Library for random numbers

## Classes

* class WINDOW():

## Methods

* def __init__(self):

## Code

Python tkinter example

    #Name
    #date
    #goal: create a program that displays random circles on the screen
    import tkinter#Library
    import  random #Library for random numbers
    
    #Global variables
    CANVAS_WIDTH = 800
    CANVAS_HEIGHT = 600
    
    class WINDOW():
        """Creates the main window that displays the random circles"""
        def __init__(self):
            """Runs when main window is created"""
            self.main_window = tkinter.Tk()
            #create canvas
            self.canvas = tkinter.Canvas(self.main_window, width = CANVAS_WIDTH, height = CANVAS_HEIGHT)
            #pack canvas
            self.canvas.pack()
    
            #create a random circle on the screen
            self.canvas.create_oval(0,0,100,100,fill="red")
            #to do - create a loop and use random variables for
            #x1, y1, x2, y2 to create random circles
            # random.randint(A, B) returns an int that is between A and B (inclusive)
    
            #start main loop
            self.main_window.mainloop()
    #Start the window
    w = WINDOW()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

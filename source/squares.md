---
title: squares
date: 2020-05-07
---
Example Python program squares.py

## Modules

* import tkinter#Library

## Classes

* class WINDOW():

## Methods

* def __init__(self):

## Code

Python tkinter example

    #Name
    #date
    #goal: create a program that displays a square using the following pattern
    """
    rbrbrb
    bbrbrb
    rrrbrb
    bbbbrb
    rrrrrb
    bbbbbb
    """
    import tkinter#Library
    
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
    
            #create the pattern here
            #remember to use a for loop - what square is drawn firts?
            #if counter%2 == 0 can determine if counter is odd or even
            #self.canvas.create_rectangle(x1,y1,x2,y2,fill="black")
            #draws a rectangle with top left corner in x1,y1 and bottom right in x2,y2
    
            #start main loop
            self.main_window.mainloop()
    #Start the window
    w = WINDOW()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

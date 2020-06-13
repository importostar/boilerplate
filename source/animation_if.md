---
title: animation_if
date: 2020-05-07
---
Example Python program animation_if.py

## Modules

* #import libraries
* import tkinter

## Classes

* class Ball(object):
* class App(object):

## Methods

* def __init__(self, canvas, *args, **kwargs):
* def move(self):
*  def __init__(self, master, **kwargs):
*  def animation(self):

## Code

Python tkinter example

    #import libraries
    #Uses http://stackoverflow.com/questions/13215215/python-tkinter-animation
    import tkinter
    
    #Set width, height, frames per second and how long to cross
    CANVAS_WIDTH = 800
    CANVAS_HEIGHT = 600
    FPS = 120
    SECONDS_TO_CROSS = 1.5
    
    #Ball class
    #Used to draw and move ball on screen
    class Ball(object):
        #initialize method
        #Precondition: canvas, arguments (x & y position),
        # keyword arguments (colour)
        #Postcondition: ball created and set in motion
        def __init__(self, canvas, *args, **kwargs):
            self.canvas = canvas
            self.id = canvas.create_oval(*args, **kwargs)
            self.vx = CANVAS_WIDTH/FPS/SECONDS_TO_CROSS
            self.vy = 0
        #move method
        #Precondition - gets current location
        #changes velocity based on if edge was hit
        #moves ball
        def move(self):
            x1, y1, x2, y2 = self.canvas.bbox(self.id)
            if x2 > CANVAS_WIDTH:
                self.vx = self.vx*-1
            if x1 < 0:
                self.vx = self.vx*-1
            self.canvas.move(self.id, self.vx, self.vy)
    
    #App class
    #controls the canvas and the objects displayed on it
    class App(object):
        #Initalize method, sets everything up
         def __init__(self, master, **kwargs):
            self.master = master
            #Create the canvas - graphics will be drawn on it
            self.canvas = tkinter.Canvas(self.master, width = CANVAS_WIDTH, height = CANVAS_HEIGHT)
            #pack the canvas so it shows up
            self.canvas.pack()
            #Create a list of ball objects - note the variables
            self.balls = [
                Ball(self.canvas, 20, 260, 120, 360, outline = 'white', fill = 'blue'),
                Ball(self.canvas, 2, 2, 40, 40, outline = 'white', fill = 'gold'),
                ]
            #Set animation to start right away (after 0 milliseconds
            self.master.after(0, self.animation)
    
        #animation function
         def animation(self):
             #loop through all the balls on the screen and move them
             for ball in self.balls:
                 ball.move()
             #set the timer to play again after the milliseconds have passed
             self.master.after(1000//FPS, self.animation)
    
    #create the main window, start the app and run the mainloop
    main_window = tkinter.Tk()
    app = App(main_window)
    main_window.mainloop()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

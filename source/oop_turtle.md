---
title: oop_turtle
date: 2020-05-07
---
Example Python program oop_turtle.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import Tkinter
* import turtle

## Classes

* class Sprite(turtle.Turtle):

## Methods

*   def __init__(self):
* def up():
* def down():
* def left():
* def right():
* def fire():

## Code

Python tkinter example

    
    # Import the Tkinter & Turtle Graphics Modules
    import Tkinter
    import turtle
    
    # Create Game Window
    screen = turtle.Screen()
    screen.screensize(500, 500, "black")
    
    # Create Sprite Object Which Inherits from Turtle
    class Sprite(turtle.Turtle):
      def __init__(self):
        turtle.Turtle.__init__(self)
    
    # Create Sprite
    screen.addshape("sprite.gif")
    mySprite = Sprite()
    mySprite.hideturtle() # hide turtle until the the duck image replaces the placeholder shape
    mySprite.penup() # prevent sprite from drawing on screen as it moves
    mySprite.left(90) # rotate sprite for proper placement on screen
    mySprite.shape("sprite.gif") # Set Image for Sprite
    mySprite.setposition(0, 0)
    mySprite.showturtle()
    
    # Create Player Controls
    def up():
        global mySprite
        mySprite.setposition(mySprite.xcor(), mySprite.ycor() + 10)
    
    def down():
        global mySprite
        mySprite.setposition(mySprite.xcor(), mySprite.ycor() - 10)
    
    def left():
        global mySprite
        mySprite.setposition(mySprite.xcor() - 10, mySprite.ycor())
    
    def right():
        global mySprite
        mySprite.setposition(mySprite.xcor() + 10, mySprite.ycor())
    
    def fire():
        print("FIRE! (space bar pressed)")
    
    # Set Event Listeners for Player Controls
    screen.onkey(up, "Up")
    screen.onkey(down, "Down")
    screen.onkey(left, "Left")
    screen.onkey(right, "Right")
    screen.onkey(fire, "space")
    screen.listen()
    
    # Main Game Loop (Keeps Game Window From Closing)
    Tkinter.mainloop()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

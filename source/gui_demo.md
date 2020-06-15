---
title: gui_demo
date: 2020-05-07
---
Example Python program gui_demo.py

## Modules

* from tkinter import *

## Methods

* def go_left():
* def go_right():
* def go_back():
* def go_forward():
* def create_arrow_buttons(frame):

## Code

Python tkinter example

    from tkinter import *
    
    
    root = Tk()
    root.title("Demo controll gui")
    
    def go_left():
        # Implement this!
        pass
    
    def go_right():
        # Implement this!
        pass
    
    def go_back():
        # Implement this!
        pass
        
    def go_forward():
        # Implement this!
        pass
    
    def create_arrow_buttons(frame):
        # Create typical arrowkey buttons using a tkinter grid.
        
        left_button = Button(frame, text="Left", command=go_left) # Creates a button inside "frame", with the title "Left", that will run the function "go_left" when clicked. 
        left_button.grid( column = 0, row = 1) # This button will be in the second row at the leftmost place of "frame"
        
        right_button = Button(frame, text="Right", command=go_right)
        right_button.grid( column = 1, row = 1)
        
        back_button = Button(frame, text="Right", command=go_back)
        back_button.grid( column = 2, row = 1)
        
        forward_button = Button(frame, text="Right", command=go_forward)
        forward_button.grid( column = 1, row = 0)
    
    
    quit_button = Button(root, text="QUIT", command=quit)
    quit_button.pack()
    
    # Just make a little space between the quit button and arrowkeys
    spacer = Frame(root, height=20)
    spacer.pack(side = TOP)
    
    # Use a frame to organice button related to the arrowkeys
    control_frame = Frame(root)
    control_frame.pack( side = BOTTOM )
    
    create_arrow_buttons(control_frame)
    
    # Let tkinter do it's thing (listen for button presses, etc)
    mainloop()
    # Clean up when quitting
    root.destroy()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

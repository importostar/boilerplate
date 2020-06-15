---
title: countdown (1)
date: 2020-05-07
---
Example Python program countdown (1).py

## Modules

* from Tkinter import *
* import ttk
* import tkFont
* #from Tkinter import font
* import time
* import datetime

## Methods

* def quit(*args):
* def show_time():

## Code

Python tkinter example

    #!/usr/bin/python
    
    from Tkinter import *
    import ttk
    import tkFont
    #from Tkinter import font
    import time
    import datetime
    
    global endTime 
    
    def quit(*args):
        root.destroy()
                
    def show_time():
        # Get the time remaining until the event
        remainder = endTime - datetime.datetime.now()
        # remove the microseconds part
        remainder = remainder - datetime.timedelta(microseconds=remainder.microseconds)
        # Show the time left
        txt.set(remainder)
        # Trigger the countdown after 1000ms
        root.after(1000, show_time)
    
    # Use tkinter lib for showing the clock
    root = Tk()
    root.attributes("-fullscreen", True)
    root.configure(background='black')
    root.bind("x", quit)
    root.after(1000, show_time)
    # Set the end date and time for the countdown
    endTime = datetime.datetime(2018, 3, 21, 0, 0, 0)
    
    #appHighlightFont = font.Font(family='He', size=12, weight='bold')
    #ttk.Label(root, text='Attention!', font=appHighlightFont).grid()
    
    #fnt = tkFont.Font(font='DS-DIGIT', size=120, weight='bold')
    txt = StringVar()
    lbl = ttk.Label(root, textvariable=txt, font=("DS-Digital", 130, "bold"), foreground="yellow", background="black")
    lbl.place(relx=0.5, rely=0.5, anchor=CENTER)
    root.mainloop()
    
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

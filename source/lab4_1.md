---
title: lab4_1
date: 2020-05-07
---
Example Python program lab4_1.py

## Modules

* import datetime
* from tkinter import *

## Code

Python tkinter example

    s = "REsult: \n"
    
    import datetime
    dt = datetime.datetime.now()
    h = int(dt.strftime("%H"))
    h = h % 12
    
    s += str("Python is structure\n")
    
    if h == 0:
        s += str("It is twelve o\'clock")
    if h == 1:
        s += str("It is one o\'clock")
    if h == 2:
        s += str("It is two o\'clock")
    if h == 3:
        s += str("It is three o\'clock")
    if h == 4:
        s += str("It is four o\'clock")
    if h == 5:
        s += str("It is five o\'clock")
    if h == 6:
        s += str("It is six o\'clock")
    if h == 7:
        s += str("It is seven o\'clock")
    if h == 8:
        s += str("It is eight o\'clock")
    if h == 9:
        s += str("It is night o\'clock")
    if h == 10:
        s += str("It is ten o\'clock")
    if h == 11:
        s += str("It is eleven o\'clock")
    
    s += str ("\n\nSwith simulation \n")
    
    switch = {
        0: "It is twelve o\'clock",
        1: "It is one o\'clock",
        2: "It is two o\'clock",
        3: "It is three o\'clock",
        4: "It is four o\'clock",
        5: "It is five o\'clock",
        6: "It is six o\'clock",
        7: "It is seven o\'clock",
        8: "It is eight o\'clock",
        9: "It is eight o\'clock",
        10: "It is ten o\'clock",
        11: "It is eleven o\'clock",
    }
    
    s += str(switch[h])
    
    # Message Box Code#######
    
    from tkinter import *
    
    root = Tk()
    root.title('Message Box')
    Label(root, justify=LEFT, text=s).grid(padx=10, pady=10)
    
    root.mainloop()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

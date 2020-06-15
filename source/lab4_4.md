---
title: lab4_4
date: 2020-05-07
---
Example Python program lab4_4.py

## Modules

* import InputBox
* from tkinter import *

## Code

Python tkinter example

    import InputBox
    from tkinter import *
    
    s = "Result:\n"
    zodiac = ""
    
    InputBox.ShowDialog("What year were you born?")
    y = int(InputBox.GetInput()) % 12
    
    s += str("\nmethod 1: if structure\n")
    
    if y == 0:
        zodiac = "Monkey"
    elif y == 1:
        zodiac = "Rooster"
    elif y == 2:
        zodiac = "Dog"
    elif y == 3:
        zodiac = "Pig"
    elif y == 4:
        zodiac = "Rat"
    elif y == 5:
        zodiac = "Ox"
    elif y == 6:
        zodiac = "Horse"
    elif y == 7:
        zodiac = "Rabbit"
    elif y == 8:
        zodiac = "Dragon"
    elif y == 9:
        zodiac = "Snake"
    elif y == 10:
        zodiac = "Horse"
    else:
        zodiac = "Goat"
    
    s += str("you were born in a " + zodiac + " year\n")
    s += str("\nMethod 2: switch sim\n")
    
    switch = {
        0: "Monkey",
        1: "Rooster",
        2: "Dog",
        3: "Pig",
        4: "Rat",
        5: "Ox",
        6: "Horse",
        7: "Rabbit",
        8: "Dragon",
        9: "Snake",
        10: "Horse",
        11: "Goat"
    }
    s += str("you were born in a " + switch[y] + " year\n")
    
    # Message Box Code#######
    
    root = Tk()
    root.title('Message Box')
    Label(root, justify=LEFT, text=s).grid(padx=10, pady=10)
    
    root.mainloop()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

---
title: lab3_4
date: 2020-05-07
---
Example Python program lab3_4.py

## Modules

* from tkinter import *

## Code

Python tkinter example

    s = "Result:\n"
    
    x = 5
    s += str(x is 5) + "\n"
    
    x = 5
    s += str(x is not 4) + "\n"
    
    x = (4, 7, 2, 1)
    tuple1 = (2 in x, 3 not in x)
    s += str(tuple1) + "\n"
    
    x = 2
    y = x
    tuple2 = (id(x), id(y))
    s += str(tuple2) + "\n"
    
    tuple3 = (x is y, x is not y)
    s += str(tuple3) + "\n"
    
    x = 3
    y = 3
    tuple4 = (id(x), id(y))
    s += str(tuple4) + "\n"
    
    tuple5 = (x is y, x is not y)
    s += str(tuple5) + "\n"
    
    x = (1, 2, 3)
    y = (1, 2, 3)
    tuple6 = (id(x), id(y))
    s += str(tuple6) + "\n"
    
    tuple7 = (x is y, x is not y)
    s += str(tuple7) + "\n"
    
    x = "apple"
    tuple8 = ('a' in x, 'a' not in x)
    s += str(tuple8) + "\n"
    
    x = [0, 1, 2, 3, 4, 5]
    tuple9 = (3 in x, 7 in x, 9 not in x, 2 not in x)
    
    s += str(tuple9) + "\n"
    
    y = (4.3, 2.1, 7.5, 3.4)
    tuple10 = (7.5 in y, 7.4 in y, 3.5 not in y, 2.1 not in y)
    s += str(tuple10) + "\n"
    
    z = ["apple", "banana", "cherry"]
    tuple11 = ("banana" in z, "Banana" in z, "Apple" not in z, "cherry" not in z)
    s += str(tuple11) + "\n"
    
    s += str(5 in range(2, 10)) + "\n"
    tuple12 = (5 & 6, 5 | 6, ~5)
    s += str(tuple12) + "\n"
    
    s += str((5|6) == (5|3)) + "\n"
    
    tuple13 = (3 << 2, 11 >> 1, 67 >> 3, 127 >> 2)
    s += str(tuple13) + "\n"
    
    ###### Message Box Code ######
    from tkinter import *
    
    root = Tk()
    root.title('Message Box')
    Label(root, justify=LEFT, text = s).grid(padx=10, pady=10)
    
    root.mainloop()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

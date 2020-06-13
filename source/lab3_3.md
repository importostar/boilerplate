---
title: lab3_3
date: 2020-05-07
---
Example Python program lab3_3.py

## Modules

* from tkinter import *

## Code

Python tkinter example

    s = "Result:\n"
    
    tuple1 = (3 < 5, "apple" < "Apple", 4 <= 5, "Orange" <= "Oranges")
    s += str(tuple1) + "\n"
    
    tuple2 = (7 > 3, "school" > "School", 3 >= 5, "tree" >= "trees")
    s += str(tuple2) + "\n"
    
    tuple3 = (6 == 7, "home" == "Home", 6 != 7, "home" != "Home")
    s += str(tuple3) + "\n"
    
    tuple4 = ('A' < 'B', "apple" < "Apple", "appLe" < "apple")
    s += str(tuple4) + "\n"
    
    s += str(ord('a')) + "\n"
    
    tuple5 = (64 == 64.0, 3e5 == 300000)
    s += str(tuple5) + "\n"
    
    a = 1
    b = 4
    s += str(a == b) + "\n"
    
    a = 5
    s += str(a < 7) + "\n"
    
    s1 = "apple"
    s += str(s1 < "orange") + "\n"
    
    a = 4
    b = 1
    tuple6 = (a < b, 3 > b)
    s += str(tuple6) + "\n"
    
    tuple7 = ((3 > 2) and (5 < 7), (3 < 2) or (5 < 7), not (3 < 2))
    s += str(tuple7) + "\n"
    
    tuple8 = (True and True, True and False, (5.3 >= 5) and (6.0 <= 6))
    s += str(tuple8) + "\n"
    
    tuple9 = (("a" < "b") and ("b" < "c"), ("a" != "") and ("a" != "a"))
    s += str(tuple9) + "\n"
    
    tuple10 = (('a' in 'apple') and ('b' not in 'apple'))
    s += str(tuple10) + "\n"
    
    tuple11 = (True or True, True or False, (3 < 4) or (4 < 5))
    s += str(tuple11) + "\n"
    
    tuple12 = ((5 in range(0, 5)) or (4 in range(0, 5)))
    s += str(tuple12) + "\n"
    
    tuple13 = (('a' == 'A'.lower()) or ('B' != 'b'.upper()))
    s += str(tuple13) + "\n"
    
    tuple14 = (not -2, not "apple", not " ", not 0, not None)
    s += str(tuple14) + "\n"
    
    ###### Message Box Code ######
    from tkinter import *
    
    root = Tk()
    root.title('Message Box')
    Label(root, justify=LEFT, text = s).grid(padx=10, pady=10)
    
    root.mainloop()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

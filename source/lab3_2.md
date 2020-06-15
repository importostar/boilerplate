---
title: lab3_2
date: 2020-05-07
---
Example Python program lab3_2.py

## Modules

* from tkinter import *

## Code

Python tkinter example

    s = "Result:\n"
    
    x = 5
    x += 4
    s += str(x) + "\n"
    
    x = 7
    x -= 4
    s += str(x) + "\n"
    
    x = 3
    x *= 2
    s += str(x) + "\n"
    
    x = 5
    x /= 4
    s += str(x) + "\n"
    
    x = 15
    x %= 7
    s += str(x) + "\n"
    
    x = 2
    x **= 3
    s += str(x) + "\n"
    
    x = 2
    x *= 5
    x *= 5
    x *= 5
    s += str(x) + "\n"
    
    x = 17.9
    x /= 3.5
    x /= 2.1
    s += str(x) + "\n"
    
    x = "An "
    x += "apple "
    x += "a day "
    x += "keeps the doctor away. "
    s += str(x) + "\n"
    
    x = 7
    x = x + 1
    s += str(x) + "\n"
    
    x += 1
    s += str(x) + "\n"
    
    x = x - 1
    s += str(x) + "\n"
    
    x -= 1
    s += str(x) + "\n"
    
    sum =0
    for i in range(10):
        sum += i
    s += str(sum) + "\n"
    
    n = 6
    f = 1
    for i in range (1, n+1):
        f *= i
    s += str(f) + "\n"
    
    ###### Message Box Code ######
    from tkinter import *
    
    root = Tk()
    root.title('Message Box')
    Label(root, justify=LEFT, text=s).grid(padx=10, pady=10)
    
    root.mainloop()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

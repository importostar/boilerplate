---
title: lab3_1
date: 2020-05-07
---
Example Python program lab3_1.py

## Modules

* from tkinter import *

## Code

Python tkinter example

    s = "Result:\n"
    
    s += str(3.5 * 4) + "\n"
    s += str("Python" * 3) + "\n"
    s += str(3 * "Python") + "\n"
    
    x = 5
    s += str(x) + "\n"
    s += str(x == 5) + "\n"
    
    s += str(3.15 + 7) + "\n"
    
    s += "Hello" + "World\n"
    
    x = 2
    y = x**3 + 4*(x * 2) + 3*x + 5
    s += str(y) + "\n"
    
    sum = 0
    for i in range(1, 11):
        sum = sum + i
    s += str(sum) + "\n"
    
    n = 6
    f = 1
    for i in range(1, n+1):
        f = f*i
    s += str(f) + "\n"
    
    s += str(3j + 5j) + "\n"
    s += str(3j - 5j) + "\n"
    s += str(3j * 5j) + "\n"
    s += str(3j / 5j) + "\n"
    s += str(3j ** 5j) + "\n"
    
    s += str(17 % 5) + "\n"
    s += str(15.9 % 4.1) + "\n"
    
    s += str(9 // 5) + "\n"
    s += str(19.4 // 5) + "\n"
    s += str(21.7 // 5.3) + "\n"
    
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

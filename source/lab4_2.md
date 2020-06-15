---
title: lab4_2
date: 2020-05-07
---
Example Python program lab4_2.py

## Modules

* import InputBox
* from tkinter import *

## Code

Python tkinter example

    s = "Result:\n"
    
    s += str("Method 1\n")
    
    import InputBox
    InputBox.ShowDialog("Enter the score [M1]: ")
    score = float(InputBox.GetInput())
    
    if score < 60 : grade = "F"
    if score >= 60 : grade = "D"
    if score >= 70 : grade = "C"
    if score >= 80 : grade = "B"
    if score >= 90 : grade = "A"
    s += str("It is a " + grade + ".\n")
    
    s += str("\nMethod 2\n")
    
    InputBox.ShowDialog("Enter the score [m2]: ")
    score = float(InputBox.GetInput())
    
    if score >= 60:
        if score >= 70:
            if score >= 80:
                if score >= 90:
                    grade = "A"
                else:
                    grade = "B"
            else:
                grade = "C"
        else:
            grade = "D"
    else:
        grade = "F"
    
    s += str("It is a " + grade + ".\n")
    
    s += str("\nMethod 3\n")
    
    InputBox.ShowDialog("Enter the score [M3]: ")
    score = (float(InputBox.GetInput()) * 100)
    if score in range(0, 6000):
        s += str("It is an F.")
    if score in range(6000, 7000):
        s += str("It is a D.")
    if score in range(7000, 8000):
        s += str("It is a C.")
    if score in range(8000, 9000):
        s += str("It is a B.")
    if score in range(9000, 10000):
        s += str("It is an A.")
    
    s += str("\nMethod 4\n")
    
    InputBox.ShowDialog("Enter the score [M4]: ")
    score = float(InputBox.GetInput())
    
    if score >= 90:
        s += str("It is an A.")
    elif score >= 80:
        s += str("It is a B.")
    elif score >= 70:
        s += str("It is a C.")
    elif score >= 60:
        s += str("It is a D.")
    else:
        s += str("It is an F.")
    
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

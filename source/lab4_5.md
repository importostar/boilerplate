---
title: lab4_5
date: 2020-05-07
---
Example Python program lab4_5.py

## Modules

* import InputBox
* from tkinter import *
* from datetime import date

## Code

Python tkinter example

    import InputBox
    from tkinter import *
    
    s = "Result:\n"
    
    InputBox.ShowDialog("enter your annual income:")
    income = float(InputBox.GetInput())
    
    if income >= 0 and income <= 25000 :
        tax_rate = 0
    elif income >= 25000 and income <= 55000 :
        tax_rate = 25
    elif income >= 55000 and income <= 105000 :
        tax_rate = 28
    elif income >= 105000 and income <= 250000 :
        tax_rate = 33
    else:
        tax_rate = 40
    
    InputBox.ShowDialog("Enter the number of dependents: ")
    depd = int(InputBox.GetInput())
    
    if depd < 3 :
        deductible = 1000
    if depd < 5 :
        deductible = 6500
    if depd > 5 :
        deductible = 10000
    switch = {
        0: "financially disadvantaged",
        25: "low-income",
        28: "middle-class",
        33: "high-income",
        40: "rich"
    }
    
    taxable = income * (1-tax_rate/100) - deductible
    if (taxable <= 0) :
        taxable = 0
    
    from datetime import date
    y = date.today().year + 1
    
    s += str("\n" + str(y) + " taxable income: " + str(round(taxable, 2)))
    
    
    s += str("\nclassification: " + switch[tax_rate])
    
    # Message Box Code#######
    
    root = Tk()
    root.title('Message Box')
    Label(root, justify=LEFT, text=s).grid(padx=10, pady=10)
    
    root.mainloop()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

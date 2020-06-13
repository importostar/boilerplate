---
title: cert
date: 2020-05-07
---
Example Python program cert.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* from tkinter import Tk
* from tkinter import *
* import tkinter as tk
* from tkinter import filedialog, Canvas, Button
* import os

## Methods

* def img():
* def excel():
* def gocontrol():

## Code

Python tkinter example

    
    
    from tkinter import Tk
    from tkinter import *
    import tkinter as tk
    from tkinter import filedialog, Canvas, Button
    import os
    
    temp_path = None
    excel_path = None
    
    window = Tk()
    window.geometry('500x500')
    
    
    
    def img():
        global temp_path
        root = tk.Tk()
        root.withdraw()
        temp_path = filedialog.askopenfilename()
        print(temp_path)
    
    
    def excel():
        global excel_path
        root = tk.Tk()
        root.withdraw()
        excel_path = filedialog.askopenfilename()
        print(excel_path)
    
    
    def gocontrol():
        print("Close This window")
        exit()
    
    
    
    
    button1 = tk.Button(window, text='Click to go Template',command=img)
    button1.grid(row=0, sticky='w')
    
    button2 = Button(window, text='Click to Excel',command=excel)
    button2.grid(row=1, sticky='w')
    
    var = StringVar(window)
    var.set("font")
    fontoption = OptionMenu(window, var, "one","two","three")
    fontoption.grid(row=2, sticky='w')
    
    buttonImp = Button(window, text='Go to Cert Generator',command=gocontrol)
    buttonImp.grid(row=3, sticky='w')
    
    #excel.locate_path
    #image.locale_path
    window.mainloop()
    print(temp_path)
    print(excel_path)
    exit()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

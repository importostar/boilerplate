---
title: CheckBoxes
date: 2020-05-07
---
Example Python program CheckBoxes.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* from tkinter import *
* from tkinter import ttk
* from tkinter.ttk import Button

## Methods

* def callback():

## Code

Python tkinter example

    from tkinter import *
    from tkinter import ttk
    from tkinter.ttk import Button
    
    root = Tk()
    def callback():
        print("ئىسمىڭىز"+entry.get())
        print("پارولىڭىز"+entry2.get())
        if chvar.get()==1:
            print(" ئەستە ساقلاڭ تاللاندى")
        else:
            print("ئەستە ساقلاڭ تاللانمىدى")
    
    
    entry = ttk.Entry(root, width=30)
    entry2 = ttk.Entry(root, width=30)
    entry.insert(0, "ئىسمىڭىزنى كىرگۈزۈڭ")
    entry2.insert(0, "پارولىڭىزنى كىرگۈزۈڭ")
    button = ttk.Button(root, text="جەزىملەش")
    lbl = ttk.Label(text="ئەسسالامۇ-ئەلەيكۇم", font=(('UKIJ Esliye'), 22))
    lblname = ttk.Label(text="ئىسمىڭىز")
    lblpass = ttk.Label(text="پارول")
    
    lbl.grid(row=0, column=0, columnspan=2)
    lblname.grid(row=1, column=0, sticky=W) # sticky=W(WEST) مەنىسى مەزكۇر ئوبىيىكتىپنىڭ ئورنىنى غەرىب تەرەپكە توغۇرلايدۇ. دېققەت ھەرپ چوڭ يېزىلىدۇ
    lblpass.grid(row=2, column=0)
    entry.grid(row=1, column=1)
    entry2.grid(row=2, column=1)
    button.grid(row=3, column=1, sticky=E+W, pady=20)# pady bolsa y oqi ustidiki arliq. padx bolsa x oqi ustidiki arliqni ipadilaydu.
    
    chvar = IntVar()
    chvar.set(0)
    cbox = Checkbutton(root, text='ئەستە ساقلاڭ', variable=chvar,
                       font=(('UKIJ Esliye'),16)).grid(row=4, column=0, sticky=E, columnspan=2)
    
    button.config(command=callback)
    root.geometry('500x450')
    root.mainloop()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

---
title: new
date: 2020-05-07
---
Example Python program new.py

## Modules

* import tkinter as tk
* from tkinter import ttk
* import Tkinter as tk
* from Tkinter import ttk

## Classes

* class App(tk.Frame):

## Methods

* def main(self):
* def __init__(self, *args, **kwargs):

## Code

Python tkinter example

    try:
        # Python 3
        import tkinter as tk
        from tkinter import ttk
    except ImportError:
        # Python 2
        import Tkinter as tk
        from Tkinter import ttk
    
    class App(tk.Frame):
        def main(self):
            # get input value
            value = self.entryValue.get()
    
            # set value to label
            self.var.set(value)
    
        def __init__(self, *args, **kwargs):
    
            root = tk.Tk()
            # ---- Label ----
            self.var = tk.StringVar()
            self.var.set("Text will appear here.")
            myLabel = tk.Label(root, textvariable= self.var)
            myLabel.pack()
    
            # ---- Entry ----
            self.entryValue = tk.StringVar(root, value="")
            self.myEntry = ttk.Entry(root,
                                        textvariable=self.entryValue)
            self.myEntry.pack()
    
            # ---- Button ----
            myButton = ttk.Button(root, text="Show Text",
                                                    command= lambda: self.main())
            myButton.pack()
    
    
            root.mainloop()
    
    myInstance = App()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

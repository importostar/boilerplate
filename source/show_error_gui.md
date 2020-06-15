---
title: show_error_gui
date: 2020-05-07
---
Example Python program show_error_gui.py

## Modules

* import tkinter
* from tkinter import messagebox

## Code

Python tkinter example

    import tkinter
    from tkinter import messagebox
    
    main_window = tkinter.Tk()
    main_window.withdraw() #remove the background window.
    
    messagebox.showinfo('Title', "This is just a text in a message box")
    messagebox.showerror('ERROR!', "Here are the details of the error that you faced right now.")
    messagebox.showwarning("WARNING!", "This will only have a button with ok as text or content.")
    messagebox.askyesno("Confirmation", "Do you really want to close the application.")
    messagebox.askokcancel("Confirm Action", "Do you want to proceed or cancel the operation?")
    messagebox.askretrycancel("Confirm Action", "Installation Failed, retry or cancel the operation?")
    
    >funnctions
    
    showinfo()
    showwarning()
    showerror ()
    askquestion()
    askokcancel()
    askyesno ()
    askretrycancel ()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

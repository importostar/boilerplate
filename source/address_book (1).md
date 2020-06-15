---
title: address_book (1)
date: 2020-05-07
---
Example Python program address_book (1).py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import tkinter

## Classes

* class MyGui:

## Methods

* def __init__(self):
* def btn_next_click(self):
* def fileopen(self):
* def filesave(self):

## Code

Python tkinter example

    #Name
    #Date
    #Add global variable - a list of addresses
    #open button should open a set text file
    #and load addresses
    #close should save using the list
    #When open first item displayed
    #next moves to next item
    import tkinter
    
    class MyGui:
        def __init__(self):
            #main window
            self.main_window = tkinter.Tk()
    
            #menus
            self.menubar = tkinter.Menu(self.main_window)
            self.filemenu = tkinter.Menu(self.main_window,tearoff=0)
            self.filemenu.add_command(label="Open", command=self.fileopen)
            self.filemenu.add_command(label="Save", command=self.filesave)
            self.filemenu.add_command(label="Exit",command=self.main_window.quit)
    
            self.menubar.add_cascade(label="File",menu=self.filemenu)
            self.main_window.config(menu = self.menubar)
    
            #frames
            self.topframe = tkinter.Frame(self.main_window)
            self.bottomframe = tkinter.Frame(self.main_window)
            self.topframe.pack()
            self.bottomframe.pack()
    
            #labels and textboxes
            self.lbl_firstname = tkinter.Label(self.topframe,text="First Name")
            self.lbl_firstname.pack(side="left")
            self.fname_text = tkinter.StringVar()
            self.fname_text.set("First name")
            self.txt_firstname = tkinter.Entry(self.topframe,text=self.fname_text)
            self.txt_firstname.pack(side="left")
    
            #buttons
            self.btn_next = tkinter.Button(self.bottomframe,text="Next",command=self.btn_next_click)
            self.btn_next.pack()
            #main loop
            tkinter.mainloop()
        def btn_next_click(self):
            self.fname_text.set("Replace with next name")
    
        def fileopen(self):
            """To-do: add code to open address
            book file. File should be:
            firstname,lastname,phone"""
            print("Open method")
        def filesave(self):
            """To-do: add code to save address
            book file."""
            print("Save method")
    
    
    gui = MyGui()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

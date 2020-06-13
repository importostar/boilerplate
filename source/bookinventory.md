---
title: bookinventory
date: 2020-05-07
---
Example Python program bookinventory.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import csv
* from tkinter import *
* import tkinter.messagebox

## Methods

* def processdata():
* def zeroprocess():

## Code

Python tkinter example

    import csv
    from tkinter import *
    import tkinter.messagebox
    
    def processdata():
        #process data, note access to tkinter variables
        uname=name.get().capitalize()
        print(uname)
        nameEntry.delete(0,END)
    
        ucopy=copies.get()
        print(ucopy)
        copyEntry.delete(0,END)
    
        print(genretype.get())
    
    def zeroprocess():
        #processes printing the division by zero
        print("Division by zero detected the universe has ended")
    
    mGui = Tk()
    
    #Vairables used by Tkinter
    genretype=StringVar()
    name=StringVar()
    copies=IntVar()
    
    #The main window controls
    mGui.geometry('450x450+50+30')
    mGui.title('Book Inventory')
    
    #Book name
    nameEntryl = Label(mGui,text='Book name:',fg='black',bg='white')
    nameEntryl.pack(pady=(5,0))
    nameEntry = Entry(mGui,textvariable=name)
    nameEntry.insert(10,"noname")
    nameEntry.pack(pady=(0,15))
    
    #Number of copies
    copyEntryl = Label(mGui,text='Number of copies:',fg='black',bg='white')
    copyEntryl.pack(pady=(0,0))
    copyEntry = Entry(mGui,textvariable=copies)
    copyEntry.insert(10,"1")
    copyEntry.pack(pady=(0,15))
    
    #Options for genre
    genreEntry1 = Label(mGui, text='Choose the books genre type',fg="black", bg="white")
    genreEntry1.pack()
    genreEntry= OptionMenu(mGui, genretype, "Science Fiction", "Sport", "Biography", "Political Thriller",)
    genreEntry.pack(pady=(0,15))
    
    #Submit data
    mbutton = Button(mGui,text="Submit",command=processdata, fg='black')
    mbutton.pack(pady=(0,15))
    
    #Division by zero
    mbutton = Button(mGui,text="Division by zero detected the universe has ended",command=zeroprocess, fg='black')
    mbutton.pack(pady=(0,15))
    
    mGui.mainloop()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

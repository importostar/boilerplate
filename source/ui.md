---
title: ui
date: 2020-05-07
---
Example Python program ui.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* from tkinter import *
* from tkinter import ttk
* from tkinter import messagebox
* from Dbconnect import  DBconnect
* from  DisplyList import  ListTicket

## Methods

* def BuSaveData():
* def buListData():

## Code

Python tkinter example

    from tkinter import *
    from tkinter import ttk
    from tkinter import messagebox
    from Dbconnect import  DBconnect
    from  DisplyList import  ListTicket
    
    dbc = DBconnect()
    root = Tk()
    root.title("Ticket")
    root.configure(background="#e1d8b2")
    # Style=
    style = ttk.Style()
    style.theme_use('classic')
    style.configure('TLabel', background="#e1d8b2")
    style.configure('TButton', background="#e1d8b2")
    style.configure('TRadiobutton', background="#e1d8b2")
    
    # full name
    ttk.Label(root, text='Full name:').grid(row=0, column=0, padx=10, pady=10)
    fullName = ttk.Entry(root, width=30, font=('Arial', 16))
    fullName.grid(row=0, column=1, columnspan=2, pady=10)
    # gander
    ttk.Label(root, text='Gander:').grid(row=1, column=0)
    SpanGender = StringVar()
    ttk.Radiobutton(root, text='Male', variable=SpanGender, value='Male').grid(row=1, column=1)
    ttk.Radiobutton(root, text='Female', variable=SpanGender, value='Female').grid(row=1, column=2)
    
    # comment
    ttk.Label(root, text='Comment:').grid(row=2, column=0)
    textComment = Text(root, width=30, height=15, font=('Arial', 16))
    textComment.grid(row=2, column=1, columnspan=2)
    # button
    BuSubmit = ttk.Button(root, text='Submit')
    BuSubmit.grid(row=3, column=3)
    BuList = ttk.Button(root, text='List Rec.')
    BuList .grid(row=3, column=2)
    
    
    # function
    def BuSaveData():
       # print("FullName{}".format(fullName.get()))
       # print("Gander{}".format(SpanGender.get()))
       #print("Comment{}".format(textComment.get(1.0, 'end')))
        dbc.Add(fullName.get(),SpanGender.get(),textComment.get(1.0, 'end'))
        messagebox.showinfo(title='Add info', message='msq')
        fullName.delete(0, 'end')
        textComment.delete(1.0, 'end')
    
    
    def buListData():
         li=ListTicket()
    
    
    BuSubmit.config(command=BuSaveData)
    BuList.config(command=buListData)
    root.mainloop()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

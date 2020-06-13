---
title: tickenter_hello
date: 2020-05-07
---
Example Python program tickenter_hello.py

## Modules

* from tkinter import *
* # from tkinter import *
* # importing only those functions
* # from tkinter import *
* # from tkinter.ttk import *

## Methods

* def clicked():

## Code

Python tkinter example

    from tkinter import *
    win = Tk()
    win.title("Hello world")
    win.geometry('400x400')
    win.iconbitmap(r"py1.ico")
    l1=Label(win,text="chintan hello", font=("Arial Bold", 20),bg='red',fg='yellow')
    
    l2=Label(win,text="cgpit",bg='green',fg='black')
    
    txt=Entry(win,width=20,bg='red',fg='white')
    
    
    def clicked():
        l2.configure(text="Button was clicked !!")
    bt=Button(win,text="click hear",bg='blue',fg='white',width=25,command=clicked)
    txt.grid(row=4)
    l1.grid(row=1)
    bt.grid(row=2)
    l2.grid(row=3)
    win.mainloop()
    
    # from tkinter import *
    # master = Tk()
    # w = Canvas(master, width=500, height=500)
    # w.pack()
    # canvas_height=4
    # canvas_width=20
    # y = int(canvas_height / 2)
    # w.create_polygon(30,10,10,80)
    # mainloop()
    
    
    # importing only those functions
    # which are needed
    # from tkinter import *
    # from tkinter.ttk import *
    #
    # # creating tkinter window
    # root = Tk()
    #
    # # Adding widgets to the root window
    # Label(root, text = 'GeeksforGeeks', font =(
    # 'Verdana', 15)).pack(side = TOP, pady = 10)
    #
    # # Creating a photoimage object to use image
    # photo = PhotoImage(file = r"py1.png")
    #
    # # here, image option is used to
    # # set image on button
    # Button(root, text = 'Click Me !', image = photo).pack(side = TOP)
    #
    # mainloop()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

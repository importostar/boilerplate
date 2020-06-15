---
title: tk
date: 2020-05-07
---
Example Python program tk.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* from tkinter import *
* from tkinter import messagebox
* import pyautogui

## Methods

* def CreateAccount(mode):
* def MsgBox(msg):

## Code

Python tkinter example

    from tkinter import *
    from tkinter import messagebox
    import pyautogui
    
    def CreateAccount(mode):
    	if mode == "Internet":
    		xycurrent = pyautogui.position()
    		print(txt1.get().isdigit())
    		print(len(txt1.get()))
    		xyimage = pyautogui.locateCenterOnScreen("C:\\Users\\Mikhail\\AppData\\Local\\Programs\\Python\\Python36-32\Scripts\\tkinter.png", region =(0, 700, 500, 68))
    		if xyimage is not None:
    			pyautogui.click(xyimage)
    			pyautogui.moveTo(xycurrent)
    
    def MsgBox(msg):
    	messagebox.showinfo('Message title', msg)
    	
    window = Tk()
    window.title("AutoGUI")
    window.geometry("300x50")
    
    menu = Menu(window)
    new_item = Menu(menu)
    new_item.add_command(label="Help", command=lambda: MsgBox("test"))
    menu.add_cascade(label="About", menu=new_item)
    window.config(menu=menu)
    
    lbl1 = Label(window, text="Create account:")
    txt1 = Entry(window, width=10)
    lbl1.grid(column=0, row=0)
    txt1.grid(column=1, row=0)
    btn1 = Button(window, width=10, text="Internet", command=lambda: CreateAccount("Internet"))
    btn1.grid(column=0, row=1)
    btn2 = Button(window, width=10, text="IP-TV", command=lambda: CreateAccount("IP-TV"))
    btn2.grid(column=1, row=1)
    
    window.mainloop()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

---
title: FileSearcher_GUI
date: 2020-05-07
---
Example Python program FileSearcher_GUI.py

## Modules

* import os
* import platform
* import pyperclip
* import sys
* import tkinter as tk
* from tkinter import * 
* import tkinter.messagebox as msg

## Methods

* def searchdir(dir):
* def file_name():

## Code

Python tkinter example

    import os
    import platform
    import pyperclip
    import sys
    import tkinter as tk
    from tkinter import * 
    import tkinter.messagebox as msg
    
    
    window=tk.Tk()
    window.title("FILE SEARCHER") # add title to your window
    window.config(bg="#9c5c92")
    
    leftFrame = Frame(window, width=300, height = 100, bg="#290323", highlightthickness=2, highlightbackground="#dec3da")
    leftFrame.grid(row=0, column=0, padx=10, pady=10, sticky=N+S)
    
    rightFrame = Frame(window, width=500, height = 100, bg="#290323", highlightthickness=2, highlightbackground="#dec3da")
    rightFrame.grid(row=0, column=1, padx=10, pady=10, sticky=N+S)
    
    tk.Label(leftFrame,text="File Name",width=10,bg="#290323",fg="#ffffff", font = ('Comic Sans MS',15)).grid(row=0,pady=5,padx=10)
    tk.Label(leftFrame,text="Directory",width=10,bg="#290323",fg="#ffffff", font = ('Comic Sans MS',15)).grid(row=3,pady=5,padx=10)
    
    e1 = tk.Entry(leftFrame,bd=3,width=35, font = ('Comic Sans MS',10))
    e2 = tk.Entry(leftFrame,bd=3,width=35,font = ('Comic Sans MS',10))
    
    e1.grid(row=0, column=1,padx=10)
    e2.grid(row=3, column=1,padx=10)
     
    path=""
    def searchdir(dir):
        FileName=e1.get()
        for (root,dirs,files) in os.walk(dir, topdown=True):
            for name in files:
                if FileName==name:
                    return os.path.join(dir,name)
            for name in dirs:
                tdir=os.path.join(root, name)
                tpath=searchdir(tdir)
                if(tpath!="0"):
                    return tpath
        return "0"
    
    def file_name():
        Directory=e2.get()
        path=searchdir(Directory)
        if path!="0":
            tk.Label(rightFrame,text=path,width=40,bg="#290323",fg="#ffffff", font = ('Comic Sans MS',15)).grid(row=0,pady=5,padx=10)
            pyperclip.copy(path)
            tk.Label(rightFrame,text="Path copied to your clipbord",width=40,bg="#290323",fg="#ffffff", font = ('Comic Sans MS',15)).grid(row=1,pady=5,padx=10)
        else:
            tk.Label(rightFrame,text="File not found in the directory",width=40,bg="#290323",fg="#ffffff", font = ('Comic Sans MS',15)).grid(row=0,pady=5,padx=10)
    
    button = tk.Button(text="Search",command=file_name,bg="#9c5c92",width=15,fg="#ffffff",font = ('Comic Sans MS',15)).grid(column=0)
    
    window.mainloop()
    
    
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

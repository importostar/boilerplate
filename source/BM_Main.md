---
title: BM_Main
date: 2020-05-07
---
Example Python program BM_Main.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* from tkinter import *   ## notice lowercase 't' in tkinter here
* import os
* from pathlib import Path
* from BM.Librry import *
* from BM.Librry import showLibrry
* from BM.newProject import form_new_project

## Methods

* def close():
* def canv_left_func(event):
* def canv_mid_func(event):
* def canv_right_func(event):
* def key(event):

## Code

Python tkinter example

    from tkinter import *   ## notice lowercase 't' in tkinter here
    import os
    from pathlib import Path
    
    from BM.Librry import *
    from BM.Librry import showLibrry
    from BM.newProject import form_new_project
    
    
    root = Tk()
    
    #get the folder dir
    
    rootPath = str(Path.home()) + str("/BM")
    
    if  not os.path.exists(rootPath):
        os.makedirs(rootPath)
    
    
    def close():
        root.destroy()
        print("Closed")
    
    #Set the form settings
    
    screen_width = root.winfo_screenwidth()
    screen_height = root.winfo_screenheight()
    screen_resolution = str(screen_width)+'x'+str(screen_height)
    
    root.geometry(screen_resolution)
    root.attributes("-fullscreen", True)
    root.title("BMI-Main")
    
    def canv_left_func(event):
        print("A"), event.x, event.y
        form_new_project()
    
    def canv_mid_func(event):
        print("B"), event.x, event.y
        showLibrry()
    
    def canv_right_func(event):
        print("C"), event.x, event.y
    
    
    def key(event):
        print ("pressed"), repr(event.char)
    
    #Create the main frame
    
    mainFrame = Frame(root,bg='red',height=300,width=600).place(relx=.5, rely=.5, anchor="center")
    
    
    
    #Canv_left obj
    
    canv_left = Canvas(mainFrame, bg='blue', height=250,width=150)
    canv_left.bind("<Key>", key)
    canv_left.bind("<Button-1>", canv_left_func)
    canv_left.place(relx=.25, rely=.5, anchor="center")
    
    
    canv_mid = Canvas(mainFrame, bg='blue', height=250,width=150)
    canv_mid.bind("<Key>", key)
    canv_mid.bind("<Button-1>", canv_mid_func)
    canv_mid.place(relx=.5, rely=.5, anchor="center")
    
    canv_right = Canvas(mainFrame, bg='blue', height=250,width=150)
    canv_right.bind("<Button-1>",key)
    canv_right.bind("<Button-1>",canv_right_func)
    canv_right.place(relx=.75, rely=.5, anchor="center")
    
    
    #form buttons
    
    exitBtn = Button(root, text="exit", command=close, bg='red')
    exitBtn.pack(anchor='n',side=RIGHT)
    
    userLbl = Label(root, text="Welcome User")
    userLbl.pack()
    
    
    #Labale for new project tab
    
    newPrj = Label(canv_left, text="New_project",bg='blue',fg='White')
    newPrj.bind("<Button-1>",key)
    newPrj.bind("<Button-1>",canv_left_func)
    newPrj.place(relx=.5, rely=.5, anchor="center")
    
    #Lable for Librry tab
    Librry = Label(canv_mid,text="Librry", bg='Blue',fg='White')
    Librry.bind("<Button-1>",key)
    Librry.bind("<Button-1>",canv_mid_func)
    Librry.place(relx=.5, rely=.5, anchor="center")
    
    #lable for the settings tab
    
    Settings = Label(canv_right, text="Settings", bg='Blue', fg='white')
    Settings.bind("<Button-1>",key)
    Settings.bind("<Button-1>",canv_right_func)
    Settings.place(relx=.5, rely=.5, anchor="center")
    
    root.mainloop()
    
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

---
title: filemanager
date: 2020-05-07
---
Example Python program filemanager.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* from tkinter import *
* from tkinter import messagebox
* from tkinter.ttk import *
* import os

## Methods

* def finder():
* def abc():
* def creater():
* def cd():

## Code

Python tkinter example

    
    from tkinter import *
    from tkinter import messagebox
    from tkinter.ttk import *
    import os
    namevar=""
    f={}
    fname="null";
    f=os.listdir(".")
    
    
    
    def finder():
        def abc():
            ad=fen.get()
            e = os.path.exists(ad)
            print(e)
            if(e==True):
                d=open(ad,'rt')
                rd=d.read()
                Label(root2,text=rd).grid(row=2,column=2)
            else:
                messagebox.showerror("Not found","File not found")
    
    
    
    
        root2=Tk()
       # newwin = Toplevel(root)
        fnm=Label(root2,text="Enter file name")
        fnm.grid(row=0,column=1)
    
        fen=Entry(root2)
        fen.grid(row=0,column=2)
    
    
    
        labelResult = Label(root2)
    
    
        labelResult.grid(row=7, column=2)
    #    opener = partial(opener, labelResult, fname)
        bn = Button(root2, text="Read", command=abc)
        bn.grid(row=1, column=3)
    
    
        root2.mainloop()
    
    def creater():
        def cd():
            fn=ade.get()
            data=df.get()
            f=open(fn,'w')
            f.write(data)
            f.close()
            messagebox.showinfo("File created","Success")
    
        root3=Tk()
        root3.title('File Creater')
        Label(root3,text="Enter the file name:").grid(row=0,column=0)
        ade=Entry(root3)
        ade.grid(row=0,column=1)
        Label(root3,text="Enter data:").grid(row=1,column=0)
        df=Entry(root3)
        df.grid(row=1,column=1)
        Button(root3,text="Create",command=cd).grid(row=2,column=1)
        root3.mainloop()
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    root=Tk()
    a="File Manager"
    root.title("File Manager")
    
    
    
    
    
    
    
    lable=Label(root,text=a)
    lable.grid(row=0,column=1)
    lable2=Label(root,text=f)
    lable2.grid(row=1,column=0)
    
    lable2=Label(root,text="Menu")
    lable2.grid(row=2,column=1)
    
    
    
    
    
    btn=Button(root,text="1.Open",command=finder)
    btn.grid(column=2,row=3)
    btn2=Button(root,text="2.Create",command=creater)
    btn2.grid(row=4,column=2)
    
    
    
    
    
    root.mainloop()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

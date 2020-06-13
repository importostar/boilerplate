---
title: replace_file
date: 2020-05-07
---
Example Python program replace_file.py

## Modules

* from tkinter import *
* import tkinter.messagebox
* import os

## Methods

* def apply(oldfile, newfile):
* def fetch(entries):
* def makeform(root, fields_defaulttxt):

## Code

Python tkinter example

    from tkinter import *
    import tkinter.messagebox
    import os
    
    
    fields_defaulttxt = [("被替换的旧文件","old.txt"), ("用于替换的新文件","new.txt")]
        
    
    def apply(oldfile, newfile):
        if not os.path.exists(oldfile) or not os.path.exists(newfile):
            tkinter.messagebox.showinfo("info", "新文件或旧文件不存在!")
        else:
            os.remove(oldfile)
            os.rename(newfile, oldfile)
    
    def fetch(entries):
        oldfile = entries[0][1].get()
        newfile = entries[1][1].get()
        apply(oldfile, newfile) 
    
    def makeform(root, fields_defaulttxt):
        Label(root, text="作用：删除旧文件，并将新文件命名为旧文件名").pack(side=TOP)
        entries = []
        for (field, defaulttxt) in fields_defaulttxt:
            row = Frame(root)
            lab = Label(row, width=15, text=field, anchor='w')
            ent = Entry(row)
            ent.insert(10, defaulttxt)
            row.pack(side=TOP, padx=5, pady=5)
            lab.pack(side=LEFT)
            ent.pack(side=RIGHT, expand=YES)
            entries.append((field, ent))
            
        return entries
    
    if __name__ == '__main__':
       root = Tk(className="替换文件")
       ents = makeform(root, fields_defaulttxt)
       root.bind('<Return>', (lambda event, e=ents: fetch(e)))   
       b1 = Button(root, text='执行',
          command=(lambda e=ents: fetch(e)))
       b1.pack(side=LEFT, padx=5, pady=5)
       b2 = Button(root, text='退出', command=root.quit)
       b2.pack(side=RIGHT, padx=5, pady=5)
       root.mainloop()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

---
title: FolderOrganizer
date: 2020-05-07
---
Example Python program FolderOrganizer.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import os
* import tkinter
* from tkinter import *

## Classes

* class DragDropListbox(tkinter.Listbox):

## Methods

* def find(needle, haystack):
* def __init__(self, master, **kw):
* def setCurrent(self, event):
* def shiftSelection(self, event):
* def update_dict(self, event):

## Code

Python tkinter example

    import os
    import tkinter
    from tkinter import *
    
    dict_names = {}
    
    def find(needle, haystack):
        for item in haystack:
            if needle in item:
                return item
        return None
    
    class DragDropListbox(tkinter.Listbox):
        """ A Tkinter listbox with drag'n'drop reordering of entries. """
        def __init__(self, master, **kw):
            kw['selectmode'] = tkinter.SINGLE
            tkinter.Listbox.__init__(self, master, kw)
            self.bind('<Button-1>', self.setCurrent)
            self.bind('<B1-Motion>', self.shiftSelection)
            self.bind('<ButtonRelease-1>', self.update_dict)
            self.curIndex = None
            
        def setCurrent(self, event):
            self.curIndex = self.nearest(event.y)
    
        def shiftSelection(self, event):
            i = self.nearest(event.y)
            if i < self.curIndex:
                x = self.get(i)
                self.delete(i)
                self.insert(i+1, x)
                self.curIndex = i
            elif i > self.curIndex:
                x = self.get(i)
                self.delete(i)
                self.insert(i-1, x)
                self.curIndex = i
                
        def update_dict(self, event):
            for index in range(self.size()):
                dict_names[index] = self.get(index)
    
    subdirs = next(os.walk('.'))[1]
    
    if len(subdirs) > 99:
        print("You can't organize over 100 projects.  Make better life choices.")
        exit()
    
    names = [None]*len(subdirs)
    lengths = [None]*len(subdirs)
    
    for i in range(len(subdirs)):
        if subdirs[i][0].isdigit() and subdirs[i][1].isdigit() and subdirs[i][2:5] == " - ":
                names[i] = subdirs[i][5:]
        elif subdirs[i][0].isdigit() and subdirs[i][1:4] == " - ":
                names[i] = subdirs[i][4:]
        else:
            names[i] = subdirs[i]
        lengths[i] = len(names[i])
        dict_names[i] = names[i]
    
    master = Tk()
    
    listbox = DragDropListbox(master, selectmode="BROWSE", width=max(lengths), height=len(names))
    for i in range(len(subdirs)):
        listbox.insert(END, names[i])
    
    listbox.pack()
    mainloop()
    
    for i, folder in enumerate(names):
        folder = find(dict_names[i], subdirs)
        if folder is None:
            print("Failed to rename ", dict_names[i])
            exit()
        else:
            prepend = "0" if len(subdirs) > 9 and i<9 else ""
            os.rename(folder, prepend+str(i+1)+" - "+str(dict_names[i]))

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

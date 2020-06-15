---
title: TKInterGUIDict_0
date: 2020-05-07
---
Example Python program TKInterGUIDict_0.py

## Modules

* from Tkinter import *  # Python 2
* # from tkinter import *  # Python 3

## Classes

* class GuiRec(Frame):  # We're going to "inherit" the Frame class. 

## Methods

* def __init__(self, master, rec):  # What happens when you initialize the GuiRec
* def update_record(self):
* def get_gui_rec(record):

## Code

Python tkinter example

    from Tkinter import *  # Python 2
    # from tkinter import *  # Python 3
    
    class GuiRec(Frame):  # We're going to "inherit" the Frame class. 
        def __init__(self, master, rec):  # What happens when you initialize the GuiRec
            Frame.__init__(self, master)  # Like any frame, you gotta set the parent.
            
            self.record = rec
            
            # You could also make these "public properties" or whatever. Your call.
            self.fields = rec.keys()
            self.fields.sort()  # for now, let's sort these alphabetically
                
            self.labels = []
            self.entries = []
            
            # We need to add a row for each key/value pair.
            # That means 1 Label and one Entry
            for i in range(len(self.fields)):
                name = self.fields[i]
    
                lbl = Label(self, text=name)
                lbl.grid(column=0, row=i)
                self.labels.append(lbl)
    
                entry = Entry(self)
                entry.insert(0, rec[name])
                entry.grid(column=1, row=i)
                self.entries.append(entry)
                
            # Then, we need an "Ok" button
            self.btnOk = Button(self, text="OK", command=self.update_record)
            self.btnOk.grid(row=len(self.fields), column=0, columnspan=2)
    
        # This is what happens when the Ok button is pressed.
        def update_record(self):
            rec = {}
            for i in range(len(self.record)):
                rec[self.fields[i]] = self.entries[i].get()  # get the updated value for each key
            self.record = rec  # update the record
            self.master.destroy()  # You only want this on popups that end the application
    
    def get_gui_rec(record):
        root = Tk()  # start a new Tk window as 'root'
        window = GuiRec(root, record)  # create the GuiRec frame
        window.pack()  # fill root with the GuiRec window
        root.mainloop()  # run that ish
        new_rec = window.record  # once the root window is destroyed, get the GuiRec.record property
        return new_rec

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

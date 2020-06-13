---
title: TKInterGUIDict_1
date: 2020-05-07
---
Example Python program TKInterGUIDict_1.py

## Modules

* from Tkinter import *  # Python 2
* # from tkinter import *  # Python 3

## Classes

* class GuiRec(Frame):

## Methods

* def __init__(self, master, rec, header=[], max_row=10):
* def get_dict(self):
* def get_gui_rec(record, header=[], max_row=10):

## Code

Python tkinter example

    from Tkinter import *  # Python 2
    # from tkinter import *  # Python 3
    
    class GuiRec(Frame):
        record = {}
        
        def __init__(self, master, rec, header=[], max_row=10):
            Frame.__init__(self, master)
            self.pack()
            self.record = rec
            
            if len(header) == len(rec):
                self.fields = header
            else:
                self.fields = rec.keys()
                self.fields.sort()
            
            rec_count = len(self.fields)
            columns = int((rec_count - 1) / max_row) + 1
            if rec_count > max_row:
                rows = max_row
            else:
                rows = rec_count
                
            self.labels = []
            self.entries = []
            
            for i in range(len(self.fields)):
                name = self.fields[i]
                col = 2 * int(i / max_row)
                row = i % max_row
    
                lbl = Label(self, text=name)
                lbl.grid(column=col, row=row)
                self.labels.append(lbl)
    
                entry = Entry(self)
                entry.insert(0, rec[name])
                entry.grid(column=(col+1), row=row)
                self.entries.append(entry)
                
            self.btnOk = Button(self, text="Return", command=self.get_dict)
            self.btnOk.grid(row=rows, column=0, columnspan=columns+1)
    
        def get_dict(self):
            rec = {}
            for i in range(len(self.record)):
                rec[self.fields[i]] = self.entries[i].get()
            self.record = rec
            self.master.destroy()
    
    def get_gui_rec(record, header=[], max_row=10):
        root = Tk()
        window = GuiRec(root, record, header=header, max_row=max_row)
        root.mainloop()
        new_rec = window.record
        return new_rec

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

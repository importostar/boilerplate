---
title: reusable_form
date: 2020-05-07
---
Example Python program reusable_form.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* from tkinter import *
* import sys

## Classes

* class Form:
* class DynamicForm(Form):

## Methods

* def __init__(self, labels, parent=None):
* def onSubmit(self):
* def onCancel(self):
* def __init__(self, labels=None):
* def onSubmit(self):

## Code

Python tkinter example

    """
    """
    from tkinter import *
    entrysize = 40
     
    class Form:
        def __init__(self, labels, parent=None):
            labelsize = max(len(x) for x in labels) + 2
            box = Frame(parent)
            box.pack(expand=YES, fill=X)
            rows = Frame(box, bd =2, relief=GROOVE)
            rows.pack(side=TOP, expand=YES, fill=X)
            self.content = {}
            for label in labels:
                row = Frame(rows)
                row.pack(fill=X)
                Label(row, text=label, width=labelsize).pack(side=LEFT)
                entry = Entry(row, width=entrysize)
                entry.pack(side=RIGHT, expand=YES, fill=X)
                self.content[label] = entry
            Button(box, text='Cancel', command=self.onCancel).pack(side=RIGHT)
            Button(box, text='Submit', command=self.onSubmit).pack(side=RIGHT)
            box.master.bind('<Return>', (lambda event: self. onSubmit()))
        def onSubmit(self):
            for key in self.content:
                print(key, '\t=>\t', self.content[key].get())
        def onCancel(self):
            Tk.quit()
     
             
    class DynamicForm(Form):    
        def __init__(self, labels=None):
            labels = input('Enter field names:').split()
            Form.__init__(self, labels)
             
        def onSubmit(self):
            print('Field Values...')
            Form.onSubmit(self)
            self.onCancel()
    if __name__ == "__main__":
        import sys
        if len(sys.argv) == 1:
            Form(['Name', 'Age', 'Job'])
        else:
            DynamicForm()
        mainloop()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

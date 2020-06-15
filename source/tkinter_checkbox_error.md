---
title: tkinter_checkbox_error
date: 2020-05-07
---
Example Python program tkinter_checkbox_error.py

## Modules

* from Tkinter import *
* import pickle, os

## Classes

* class Tickbox(object):

## Methods

* 	def __init__(self, building, row_num, col_num, save_name):
* def saveCoords():

## Code

Python tkinter example

    # What I want to happen:
    # 1. Select 'Setting 1', 'Setting 4'.
    # 2. Click save button.
    # 3. Close and reopen file.
    # 4. See that 'Setting 1' and 'Setting 4' are already selected.
    #
    # What actually happens:
    #
    # 1-3. No problems.
    # 4. No setting boxes are already selected.
    # 5. Manually select 'Setting 1'. 'Setting 4' activates by itself.
    # 6. Manually select 'Setting 2'. "Setting 3' activates by itself.
    #
    # I've used this method before to call up saved text and integers in Tkinter.Label() without problems.  
    # I don't know where to start looking to see where the difference lies. 
    # Is it IntVar()? Is it Tkinter.Checkbox()?
    
    
    from Tkinter import *
    import pickle, os
    
    FILE_NAME = "var_save.txt"
    
    if os.path.isfile(FILE_NAME) == True:
    	NEW_DIC = pickle.load(open(FILE_NAME, 'r'))
    else:
    	NEW_DIC = {}
    
    master = Tk()
    
    class Tickbox(object):
    	def __init__(self, building, row_num, col_num, save_name):
    		global NEW_DIC
    		if NEW_DIC != {}:
    			self.var = NEW_DIC[save_name]
    		else:
    			self.var = IntVar()
    		
    		self.c = Checkbutton(master, text= str(building), variable=self.var)
    		self.c.grid(row = row_num, column = col_num, sticky = W)
     
    def saveCoords():
    	preferences = {
    	'var1': var1.var.get(),
    	'var2': var2.var.get(),
            'var3': var3.var.get(),
    	'var4': var4.var.get(),
    	}
    	
    	file_name = "var_save.txt"
    	if os.path.isfile(file_name) == True:
    		fileObject = open(file_name, 'r + a')
    	else:
    		fileObject = open(file_name, 'w')
    	pickle.dump(preferences, fileObject)
    	fileObject.close
     
    var1 = Tickbox("Setting 1", 0, 0, 'var1')
    var2 = Tickbox("Setting 2", 0, 1, 'var2')
    var3 = Tickbox("Setting 3", 1, 0, 'var3')
    var4 = Tickbox("Setting 4", 1, 1, 'var4')
     
    save_button = Button(master, text="Save", command=saveCoords)
    save_button.grid(row = 2, column = 0)
     
    mainloop()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

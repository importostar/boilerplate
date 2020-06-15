---
title: folderadder (1)
date: 2020-05-07
---
Example Python program folderadder (1).py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* from __future__ import print_function #import modern python3 stuff into python2
* from tkinter import filedialog, messagebox #use the tkinter gui toolkit and dialoges
* import os, tkinter #import OS functions

## Code

Python tkinter example

    # WORKS ON PYTHON 2.7 AND 3.x
    from __future__ import print_function #import modern python3 stuff into python2
    from tkinter import filedialog, messagebox #use the tkinter gui toolkit and dialoges
    import os, tkinter #import OS functions
    
    ### SET THE SUB-FOLDER NAME YOU WANT TO ADD TO
    ### ALL YOUR FOLDERS HERE:
    
    subfoldername = "changeme"
    
    ##################################################
    
    #GUI setup
    root = tkinter.Tk() #set up the basic tkinter window
    root.withdraw() #hide the default empty window
    
    #use a message box to tell user what to do
    messagebox.showinfo("Lazy Newb Folder Adder", "Go inside the folder you need\nthat contains your folders to\nadd subfolders to")
    dirlocation = filedialog.askdirectory() #open the file chooser, and save the result
    dirs = next(os.walk(dirlocation))[1] #get the first column in a info list of directories and store it
    
    #loop through each directory one after another and add a subfolder to it
    for i in dirs:
        print(dirlocation + i + "/" + subfoldername)
        #use try/except so if it fails to make a directory (because it exists), that it keeps going without quitting
        try:
            os.makedirs(dirlocation + "/" + i + "/" + subfoldername)
            
            #print any errors as it keeps going
        except Exception as e:
            print(e)

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

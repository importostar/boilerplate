---
title: browse_folder_button_labels
date: 2020-05-07
---
Example Python program browse_folder_button_labels.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* # Test if Python2, if error import python3 modules
* from Tkinter import *
* import tkFileDialog as filedialog
* from tkinter import *
* from tkinter import filedialog
* import os

## Methods

* def browse_button():

## Code

Python tkinter example

    """
    Example of tkinter code to generate a window with a browse button
    to select a directory. Compatible with Python27 and 37
    Derived from https://stackoverflow.com/questions/43516019/python-tkinter-browse-folder-button
    """
    
    
    # Test if Python2, if error import python3 modules
    try:
        from Tkinter import *
        import tkFileDialog as filedialog
        
    except ImportError:
        from tkinter import *
        from tkinter import filedialog
    
    
    import os
        
    def browse_button():
        # Allow user to select a directory and store it in global var
        # called folder_path (can be then used outside of the function)
        global folder_path
        # The title will appear in the pop up window when selecting directory
        filename = filedialog.askdirectory(initialdir=os.getcwd(), title='Please select input directory')
        folder_path.set(filename)
        print(filename)
    
    # create root
    root = Tk()
    
    # Create Tkinter variable
    folder_path = StringVar()
    
    # Display first the lbl0, then the button2, then the lbl1
    
    # Create text before the button
    lbl0 = Label(master=root, text="Choose input directory")
    lbl0.grid(row=0, column=0)
    
    # Create a place for the name of the directory once it will be assigned 
    # with the function browse_button
    lbl1 = Label(master=root,textvariable=folder_path)
    lbl1.grid(row=0, column=2)
    
    # Create button to search for directory and call browse_button command
    button2 = Button(text="Browse", command=browse_button)
    button2.grid(row=0, column=1)
    
    # Launch main loop
    mainloop()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

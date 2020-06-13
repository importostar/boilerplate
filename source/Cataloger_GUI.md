---
title: Cataloger_GUI
date: 2020-05-07
---
Example Python program Cataloger_GUI.py

## Modules

* from tkinter import filedialog
* from tkinter import *
* from tkinter.ttk import *
* import ntpath
* import Cataloger_v3

## Methods

* def openfile():

## Code

Python tkinter example

    from tkinter import filedialog
    from tkinter import *
    from tkinter.ttk import *
    import ntpath
    import Cataloger_v3
    
    window = Tk()
    window.geometry("800x600")
    window.title("Item to Product Cataloger")
    window.iconbitmap(r"C:/Users/Vetcove/Downloads/catalog_icon.ico")
    
    
    #------GLOBAL VARIABLES-----
    
    file_name= "example.xlsx"
    
    
    #------FUNCTIONS-----
    
    def openfile():
    	global file_name
    	file_path = filedialog.askopenfilename(initialdir = "/",title = "Select file",filetypes = (("Microsoft Excel Worksheet","*.xlsx"),("All Files","*.*")))
    	list_of_path_values = file_path.split("/")
    	file_name = list_of_path_values[len(list_of_path_values)-1]
    	file_var.set(file_name)
    
    #------LABELS-----
    file_var = StringVar()
    l1 = Label(window, text = "Welcome to Item to Product Cataloger", font = ("", 18, "bold"))
    l2 = Label(window, text = "*DISCLAIMER*", font = ("", 12, "bold"))
    l3 = Label(window, text = "This program does not complete the entire item to product process and is only a tool to make certain steps more efficient. THIS TOOL DOES NOT REPLACE THE NEED FOR \"CLEAN UP \". Please be sure to check over any changes and make any necessary changes. Also be sure to make a copy of the original file in case of any undesireable outcomes. See Source Code for more information about what the program can/cannot do. Always open for improvements! Thank You!", font = ("", 12), wraplength = 760)
    l4 = Label(window, text = "Instructions:", font = ("", 12, "bold"))
    l5 = Label(window, text = "Ensure that the file you want to modify is closed and in the same folder as this tool. Also ensure that there is an example.xlsx file (content doesn't matter, just has to be called \"example.xlsx\" in the same folder. Ensure that the file is formatted in the proper orientation for cataloging (item name in column B and product name in column D).", font = ("", 12), wraplength = 760)
    l6 = Label(window, text = "1. Click \"Choose File to Format\" to select a file for cataloging", font = ("", 12))
    l7 = Label(window, text = "2. Click \" Start\" and let this tool save hours of your time! Wait 30 seconds for the tool to complete its job!", font = ("", 12))
    
    file_label = Label(window, textvariable = file_var, font = ("", 12)).place(relx = 0.5, rely = 0.65, anchor = CENTER)
    
    l1.place(relx = 0.5, rely = 0.1, anchor = CENTER)
    l2.place(relx = 0.5, rely = 0.15, anchor = CENTER)
    l3.place(relx = 0.5, rely = 0.25, anchor = CENTER)
    l4.place(relx = 0.5, rely = 0.35, anchor = CENTER)
    l5.place(relx = 0.5, rely = 0.425, anchor = CENTER)
    l6.place(relx = 0.5, rely = 0.50, anchor = CENTER)
    l7.place(relx = 0.5, rely = 0.55, anchor = CENTER)
    #-----ENTRIES-----
    
    #-----BUTTONS-----
    
    filebutton = Button(window, text='Choose File to Format', command= openfile).place(relx = 0.5, rely = 0.6, anchor = CENTER)
    
    Button(window, text='Start', command= Cataloger_v3.main_to_export(file_name)).place(relx = 0.5, rely = 0.7, anchor = CENTER)
    Button(window, text='Quit', command= window.quit).place(relx = 0.95, rely = 0.95, anchor = E)
    
    window.mainloop()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

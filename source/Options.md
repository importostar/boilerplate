---
title: Options
date: 2020-05-07
---
Example Python program Options.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* from tkinter import *
* from tkinter import messagebox
* from tkinter.filedialog import askopenfilename
* import pandas as pd 

## Code

Python tkinter example

    from tkinter import *
    from tkinter import messagebox
    from tkinter.filedialog import askopenfilename
    import pandas as pd 
    
    
    
    
    window = Tk() 
    window.wm_title("Sampler")
    
    # l1 = Label(window,text="Select the sheet you want to parse from")
    # l1.grid(row = 0 , column = 0 , padx=30, pady=30) 
    df = pd.ExcelFile("test.xlsx")
    arr_of_excel_sheets = df.sheet_names
    print(type(arr_of_excel_sheets))
    choices = arr_of_excel_sheets
    myCh = StringVar(window)
    myCh.set(arr_of_excel_sheets[0])
    # sheetMenu = OptionMenu(window,myCh,*choices)
    # sheetMenu.grid(row=1,column=0,padx=30,pady=30)
    # print(myCh.get())
    
    df1 = pd.read_excel("test.xlsx",sheet_name="test1")
    col_names= list(df1.columns.values.tolist())
    
    print(type(col_names))
    
    l2 = Label(window,text="Select sections you want to copy")
    
    values = StringVar()
    values.set(col_names)
    
    lstbox = Listbox(window, listvariable=values, selectmode=MULTIPLE, width=20, height=10)
    lstbox.grid(column=2, row=0, columnspan=2)
    
    window.geometry("500x500")
    window.resizable(0,0)
    window.mainloop()
    
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

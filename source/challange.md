---
title: challange
date: 2020-05-07
---
Example Python program challange.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* from tkinter import *
* import tkinter.messagebox
* from openpyxl import load_workbook
* import xlwt  
* import xlrd
* from xlwt import Workbook 

## Methods

* def saving():
* def showing():

## Code

Python tkinter example

    from tkinter import *
    import tkinter.messagebox
    from openpyxl import load_workbook
    import xlwt  
    import xlrd
    from xlwt import Workbook 
    task_manager = Tk()
    task_manager.title('Task Manager')
    task_manager.geometry('250x100')
    Label(task_manager,text=('Name of the task'),padx=0).grid(row=1)
    Label(task_manager,text=(' The deadline'),padx=0).grid(row=2)
    place1=Entry(task_manager)
    place2=Entry(task_manager)
    place1.grid(row=1, column=1)
    place2.grid(row=2, column=1)
    def saving():
        saving_file = load_workbook('example.xlsx')
        sheet = saving_file.get_sheet_by_name('Sheet1')
        last_added=int(sheet.max_row)+1
        print(last_added)
        sheet.cell(row=last_added, column=1).value=place1.get()
        sheet.cell(row=last_added, column=2).value=place2.get()
        saving_file.save('example.xlsx') 
        tkinter.messagebox.showinfo("saving", "The task is saved")
    def showing():
        task_dic={}
        counter=int(sheet.max_row)
        saving_file = load_workbook('./example.xlsx')
        sheet = saving_file.get_sheet_by_name('Sheet1')
        for i in range(1, counter):
            task_time=sheet.cell(row=i, column=2).value
            task_name=sheet.cell(row=i, column=1).value
            task_dic[task_name]=task_time
        tkinter.messagebox.showinfo("the current tasks", "The current tasks are \n"+str(task_dic))
    save= Button(task_manager,text="save",width=12, command=saving)
    save.grid(row=3, column=1)
    show= Button(task_manager,text="show",width=12, command=showing)
    show.grid(row=4, column=1)
    task_manager.mainloop()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

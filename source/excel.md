---
title: excel
date: 2020-05-07
---
Example Python program excel.py
For Python version 2.x.
To test your Python version use:

    python --version

## Modules

* from Tkinter import *
* from xlrd import open_workbook
* import Tkinter
* import tkFileDialog

## Methods

* def dirname(): 
* def file(): 

## Code

Python tkinter example

    from Tkinter import *
    from xlrd import open_workbook
    import Tkinter
    import tkFileDialog
     
    ventana = Tk()
    ventana.title('Reportes Telcel')
    label1=Label(ventana,text="Reportes Telcel")
    label1.grid(row=100,column=100) 
    
    def dirname(): 
     tkFileDialog.askdirectory(parent=ventana,initialdir="/",title='Please Select a directory')
    
    def file(): 
     archivo = tkFileDialog.askopenfile(parent=ventana, mode='rb',title='Choose a file')
     aString1 = open_workbook(archivo.name)
     print "Numero de paginas: ", aString1.nsheets
     print "Nombre de las paginas", aString1.sheet_names()
    
    variable_string = StringVar()
    caja = Entry(ventana, textvariable=variable_string)
    caja.grid(row=115, column=100)
     
    boton1 = Tkinter.Button(ventana,text="Examinar", command=file)
    boton1.grid(row=115,column=125)
     
    variable_string = StringVar()
    caja1 = Entry(ventana, textvariable=variable_string)
    caja1.grid(row=125, column=100)
     
    boton2 = Tkinter.Button(ventana,text="Examinar", command=file)
    boton2.grid(row=125,column=125)
     
    # aString = open_workbook("example.xls")
    # print "Numero de paginas: ", aString.nsheets
    # print "Nombre de las paginas", aString.sheet_names()
     
     
    boton3 = Tkinter.Button(ventana,text="Comparar")
    boton3.grid(row=150,column=100)
    
    ventana.mainloop()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

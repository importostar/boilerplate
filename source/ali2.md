---
title: ali2
date: 2020-05-07
---
Example Python program ali2.py
For Python version 2.x.
To test your Python version use:

    python --version

## Modules

* from Tkinter import *
* from xlrd import open_workbook,XL_CELL_TEXT,empty_cell
* import Tkinter
* import tkFileDialog

## Methods

* def dirname(): 
* def filesegundo():
* def file(): 
* def comparar():
* """def variable_global_comparar():
* """def comparar():
* 	#def compare():

## Code

Python tkinter example

    from Tkinter import *
    from xlrd import open_workbook,XL_CELL_TEXT,empty_cell
    import Tkinter
    import tkFileDialog
    
    print empty_cell.value
    
    nombrecelda = 0
    nombrecelda2 = 0
    
    ventana = Tk()
    ventana.title('Reportes Telcel')
    label1=Label(ventana,text="Reportes Telcel")
    label1.grid(row=100,column=100)
    
    
    def dirname(): 
    	tkFileDialog.askdirectory(parent=ventana,initialdir="/",title='Please Select a directory')
    
    def filesegundo():
    	archivo = tkFileDialog.askopenfile(parent=ventana, mode='rb',title='Choose a file')
    	aString1 = open_workbook(archivo.name)
    	sheet = aString1.sheet_by_index(0)
    	#empty = sheet.cell(0,2)
    	#blank = sheet.cell(0,2)
    	nombrecelda2 = sheet.cell(1,0).value
    	global nombrecelda2
    	print nombrecelda2
    	print "Numero de paginas:", aString1.nsheets
    	print "Nombre de las paginas:", aString1.sheet_names()
    #extrae el nombre de la columna del archivo elegido
    def file(): 
    	archivo = tkFileDialog.askopenfile(parent=ventana, mode='rb',title='Choose a file')
    	aString1 = open_workbook(archivo.name)
    	sheet = aString1.sheet_by_index(0)
    	#empty = sheet.cell(0,2)
    	#blank = sheet.cell(0,2)
    	nombrecelda = sheet.cell(1,0).value
    	global nombrecelda
    	print nombrecelda
    	print "Numero de paginas:", aString1.nsheets
    	print "Nombre de las paginas:", aString1.sheet_names()
    	# print cell.ctype==XL_CELL_TEXT
    	# print sheet.ncols
    	# for i in range(sheet.ncols):
    	# 	print sheet.cell_type(0,i),sheet.cell_value(0,i)
    
    def comparar():
    	if nombrecelda == nombrecelda2:
    		print "el nombre es igual"
    	else:
    		print "no lo soy"
    
    """def variable_global_comparar():
    
    	n1=boton1.get(aString1)
    	n2=boton2.get(aString1)
    
    
    	if n1==n2:
    		print "las columnas son iguales."
    
    	else:
    
    		print result.ncols
    		wb.save('new.xls')
    """
    variable_string = StringVar()
    caja = Entry(ventana, textvariable=variable_string)
    caja.grid(row=115, column=100)
    
    boton1 = Tkinter.Button(ventana,text="Examinar", command=file)
    boton1.grid(row=115,column=125)
    
    
    variable_string = StringVar()
    caja1 = Entry(ventana, textvariable=variable_string)
    caja1.grid(row=125, column=100)
    
    boton2 = Tkinter.Button(ventana,text="Examinar", command=filesegundo)
    boton2.grid(row=125,column=125)
    
    
    
    boton3 = Tkinter.Button(ventana,text="Comparar",command=comparar)
    boton3.grid(row=150,column=100)
    
    """def comparar():
    
    n1=string(boton1.get())
    n2=string(boton2.get())
    
    compara = """
    
    """
    #book=open_workbook('example2.xls')
    #sheet = book.sheet_by_index(0)
    
    #cell = sheet.cell(0,0)
    #print cell.ctype==XL_CELL_TEXT
    
    #for i in range(sheet.ncols):
    #		print sheet.cell_type(0,i),sheet.cell_value(0,i)
    
    
    
    #book1=open_workbook('example.xls')
    #sheet1 = book.sheet_by_index(0)
    
    #cell1 = sheet1.cell(0,0)
    #print cell1.ctype==XL_CELL_TEXT
    
    #for i in range(sheet.ncols):
    #		print sheet1.cell_type(0,i),sheet1.cell_value(0,i)
    
    
    
    
    """
    """for i in range(sheet.ncols):
    		print sheet.cell_type(0,i),sheet.cell_value(0,i)
    
    	print empty is blank, empty is empty_cell, blank is empty_cell
    	
    	print empty.ctype,repr(empty.value)
    	print blank.ctype,repr(blank.value)
    
    
    
    
    #Definir variables para comparar Excel
    	
    	#comp = 0	
    	#def compare():
    	#if campo1 == campo2 || cell_value !=0 && cell_value !=S/SA
    		#print sheet.cell_values(0,0)
    
    	#else if 
    	#valor1 != valor2
    	#	print sheet.cell_values(0,0) insert into('excel3.xls')		
    
    		
    		#global comp
    
    	#campo1 = archivo.get('Cuenta')
    	#campo2 = archivo.get('Cuenta')
    """
    
    
    ventana.mainloop()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

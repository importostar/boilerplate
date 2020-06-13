---
title: ExcelAli
date: 2020-05-07
---
Example Python program ExcelAli.py
For Python version 2.x.
To test your Python version use:

    python --version

## Modules

* from Tkinter import *
* from xlrd import open_workbook,XL_CELL_TEXT,empty_cell
* import Tkinter
* import tkFileDialog
* import Image
* import  xlwt
* import time
* from xlutils.copy import copy
* from xlwt import easyxf
* import sys

## Classes

* class User(object):

## Methods

* 	def __init__(self, indice, id):
* def dirname():					
* def file():
* def filesegundo():
* def comparar():

## Code

Python tkinter example

    from Tkinter import *
    from xlrd import open_workbook,XL_CELL_TEXT,empty_cell
    import Tkinter
    import tkFileDialog
    import Image
    import  xlwt
    import time
    from xlutils.copy import copy
    from xlwt import easyxf
    
    import sys
    reload(sys)
    sys.setdefaultencoding("utf-8")
    
    class User(object):
    	"""docstring for User"""
    	def __init__(self, indice, id):
    		self.indice = indice
    		self.id = id
    
    
    print empty_cell.value
    primerexcel = 0
    segundoexcel = 0
    nombrecelda = 0
    nombrecelda2 = 0
    cell = 0
    cell2 = 0
    fill = 0
    fill2 = 0
    s = 0
    
    ventana = Tk()
    ventana.title('Reportes Telcel')
    style0= xlwt.easyxf('font:name Times New Roman, colour red, bold on')
    sumar = 1 + 1
    
    
    wb = xlwt.Workbook()
     
    #codigo funcionamiento
    def dirname():					
    	tkFileDialog.askdirectory(parent=ventana,initialdir="/",title='Please Select a directory')
    
    def file():
    	archivo = tkFileDialog.askopenfile(parent=ventana, mode='rb',title='Choose a file')
    	print archivo.name
    	global primerexcel
    	primerexcel = archivo
    
    def filesegundo():
    	archivo = tkFileDialog.askopenfile(parent=ventana, mode='rb',title='Choose a file')
    	print archivo.name
    	global segundoexcel
    	segundoexcel = archivo
    
    def comparar():
    	print primerexcel.name
    	print segundoexcel.name
    
    	arreglodeobjetosid = []
    	work1 = open_workbook(primerexcel.name,formatting_info=True)	
    	work2 = open_workbook(segundoexcel.name,formatting_info=True)
    
    	wb = xlwt.Workbook()
    
    	for q in xrange(0,work1.nsheets):
    		sheet = work1.sheet_by_index(q)
    		sheetdu = work2.sheet_by_index(q)		
    	
    		ws = wb.add_sheet('R'+str(q),cell_overwrite_ok=True)
    
    		rengi = 0
    		if sheet.ncols > sheetdu.ncols:
    			rengi = sheet.ncols
    		else:
    			rengi = sheetdu.ncols
    
    		for x in xrange(3,sheetdu.nrows):
    			idi =  sheetdu.cell_value(x,3)
    			usuario = User(x,idi)
    			if len(str(idi)) != 0:
    				arreglodeobjetosid.append(usuario)
    		
    		for x in xrange(3,sheet.nrows):
    			acomparar = sheet.cell_value(x,3)
    			xfx = sheet.cell_xf_index(x, 3)
    			xf = work1.xf_list[xfx]
    			bgx = xf.background.pattern_colour_index
    			for b in xrange(0,len(arreglodeobjetosid)-1):
    				if len(str(arreglodeobjetosid[b].id)) != 0:
    					if str(acomparar) == str(arreglodeobjetosid[b].id):
    						indiceguardado = arreglodeobjetosid[b].indice
    						otrilla = rengi - 1
    						for t in xrange(0,otrilla):
    							try:
    								cabecera = sheet.cell_value(1,t)
    							except Exception, e:
    								cabecera = 0
    							
    							ws.write(1,t,sheet.cell_value(1,t))
    							try:
    								cabecerasegunda = sheetdu.cell_value(1,t)
    							except Exception, e:
    								cabecera = 0
    																
    							if cabecera == cabecerasegunda:
    								valorainsertar = sheetdu.cell_value(indiceguardado,t)	
    							else:
    								valorainsertar = 0
    							ws.write(indiceguardado,t,valorainsertar)
    						arreglodeobjetosid.remove(arreglodeobjetosid[b])
    						print len(arreglodeobjetosid)
    						break;
    					# else:
    					# 	indiceguardado = x
    					#  	idiridi = acomparar
    					#  	if len(str(idiridi)) != 0:					 		
    					# 	 	ws.write(indiceguardado,3,idiridi)
    					# 	 	for otra in xrange(0,2):
    					# 	 		ws.write(indiceguardado,otra,0)
    					# 	 	for upto in xrange(4,sheetdu.ncols):
    					# 	 		ws.write(indiceguardado,upto,0)
    					
    		print "Se agregaron los restantes"
    		print len(arreglodeobjetosid)
    		limite = sheet.nrows
    		for k in xrange(0,len(arreglodeobjetosid)-1):
    			inserti =  arreglodeobjetosid[k].id
    			try:
    				insertinum = int(inserti)
    				print insertinum
    				indice = arreglodeobjetosid[k].indice
    				for posi in xrange(0,sheetdu.ncols):
    					ws.write(limite,posi,sheetdu.cell_value(indice,posi))
    				limite = limite + 1
    			except Exception, e:
    				continue
    		arreglodeobjetosid = []
    	wb.save('result.xls')
    	print "Terminado"
    
    #Interfaz Grafica
    
    variable_string = StringVar()
    global caja
    caja = Entry(ventana, textvariable=variable_string)
    caja.grid(row=1000,column=100)
    
    variable_string = StringVar()
    global caja1
    caja1 = Entry(ventana, textvariable=variable_string)
    caja1.grid(row=1100,column=100)
     
    boton1 = Tkinter.Button(ventana,text="Examinar1", command=file)
    boton1.grid(row=1000,column=120)
    
    boton2 = Tkinter.Button(ventana,text="Examinar2", command=filesegundo)
    boton2.grid(row=1100,column=120)
     
    boton3 = Tkinter.Button(ventana,text="Comparar",command=comparar)
    boton3.grid(row=4000,column=100)
    
    photo = PhotoImage(file='Imagen2.gif',width=470, height=115)
    label1=Label(ventana, image=photo)
    label1.grid(row=100,column=100)
    
    ventana.geometry("600x500") 
    ventana.mainloop()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

---
title: FigurasTkinter
date: 2020-05-07
---
Example Python program FigurasTkinter.py

## Modules

* from Tkinter import *

## Methods

* def mostrar(num):
* def ocultar(ventana):ventana.destroy()
* def ejecutar(f):v0.after(200,f)

## Code

Python tkinter example

    # -*- coding: utf-8 -*-
    #figuras con tkinter
    
    from Tkinter import *
    
    v0 = Tk()
    v0.title('Ventana principal')
    
    
    
    v0.config(bg='green')      #fondo  bg color
    v0.geometry("500x500")
    
    
    def mostrar(num):
        v1 = Toplevel(v0)                      #VENTANA HIJA
        v1.title("Ventana hija")
        v1.protocol('wn_DELETE_WINDOW', "onexit")   #SE CIERRE CON LA CRUZ LA VENTANA
        v1.geometry('300x300')    #tamaño de la ventana
        if num == 1:
            canvas1=Canvas(v1,width=200,height=200, bg='white')     #OBJETO DE LA TKINTER   CANVAS(FIGURAS)     200 pixeles de ancho 200 ancho
            canvas1.pack(expand=YES,fill=BOTH)       #DESPLEGAR EL CANVAS, EXPAND QUE SEA EXPANDIBLE
            canvas1.create_line(10,200,200,10, width = 10, fill='purple')
    
        elif num == 2:
            canvas2=Canvas(v1,width=200,height=200, bg='white')     #OBJETO DE LA TKINTER   CANVAS(FIGURAS)     200 pixeles de ancho 200 ancho
            canvas2.pack(expand=YES,fill=BOTH)       #DESPLEGAR EL CANVAS, EXPAND QUE SEA EXPANDIBLE
            canvas2.create_rectangle(10,200,200,10, width = 10, fill='purple')
    
    
    #circulo
        elif num == 3:
            canvas3 = Canvas(v1, width=200, height=200,bg='white')  # OBJETO DE LA TKINTER   CANVAS(FIGURAS)     200 pixeles de ancho 200 ancho
            canvas3.pack(expand=YES, fill=BOTH)  # DESPLEGAR EL CANVAS, EXPAND QUE SEA EXPANDIBLE
            canvas3.create_oval(10, 200, 200, 10, width=10, fill='purple')
    
    
    def ocultar(ventana):ventana.destroy()
    def ejecutar(f):v0.after(200,f)
    
    
    #V0 donde se va desplegar el boton
    b1=Button(v0,text='Abrir ventana con linea',command=lambda:ejecutar(mostrar(1)))
    b1.grid(row=1,column=1)  #desplegar boton
    
    b2=Button(v0,text='Abrir ventana cuadro',command=lambda:ejecutar(mostrar(2)))
    b2.grid(row=1,column=2)  #desplegar boton
    
    b3=Button(v0,text='Abrir ventana circulo',command=lambda:ejecutar(mostrar(3)))
    b3.grid(row=1,column=3)  #desplegar boton
    v0.mainloop()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

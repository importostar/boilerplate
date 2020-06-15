---
title: choosertkinter
date: 2020-05-07
---
Example Python program choosertkinter.py

## Modules

* from Tkinter import *
* import tkColorChooser #libreria para obtener la gama de colores

## Methods

* def mostrar(num):
* def ocultar(ventana): ventana.destroy()
* def ejecutar(f): v0.after(200, f)

## Code

Python tkinter example

    # -*- coding: utf-8 -*-
    # figuras con tkinter
    
    from Tkinter import *
    import tkColorChooser #libreria para obtener la gama de colores
    
    v0 = Tk()
    v0.title('Ventana principal')
    v0.config(bg='green')  # fondo  bg color
    v0.geometry("800x500")
    v0.iconbitmap("descarga.ico")
    
    def mostrar(num):
        a= tkColorChooser.askcolor()     #aparece la gama de colores   RGB o numero hexadecimal
    
    
        v1 = Toplevel(v0)  # VENTANA HIJA
        v1.title("Ventana hija")
        v1.protocol('wn_DELETE_WINDOW', "onexit")  # SE CIERRE CON LA CRUZ LA VENTANA
        v1.geometry('300x300')  # tamaño de la ventana
    
        if num == 1:
            canvas1 = Canvas(v1, width=200, height=200,bg='white')  # OBJETO DE LA TKINTER   CANVAS(FIGURAS)     200 pixeles de ancho 200 ancho
            canvas1.pack(expand=YES, fill=BOTH)  # DESPLEGAR EL CANVAS, EXPAND QUE SEA EXPANDIBLE
            canvas1.create_line(10, 200, 200, 10, width=10, fill=(a[1]))    #debe llevar gato y puede ser mayuscula o minuscula
    
        #ff0000 hexadecimal
        #255,0,0
    
    
        elif num == 2:
            canvas2 = Canvas(v1, width=200, height=200,bg='white')  # OBJETO DE LA TKINTER   CANVAS(FIGURAS)     200 pixeles de ancho 200 ancho
            canvas2.pack(expand=YES, fill=BOTH)  # DESPLEGAR EL CANVAS, EXPAND QUE SEA EXPANDIBLE
            canvas2.create_rectangle(10, 200, 200, 10, width=10, fill=(a[1]))
    
    
        # circulo
        elif num == 3:
            canvas3 = Canvas(v1, width=200, height=200, bg='white')  # OBJETO DE LA TKINTER   CANVAS(FIGURAS)     200 pixeles de ancho 200 ancho
            canvas3.pack(expand=YES, fill=BOTH)  # DESPLEGAR EL CANVAS, EXPAND QUE SEA EXPANDIBLE
            canvas3.create_oval(10, 200, 200, 10, width=10, fill=(a[1]))
            # poligono
    
        elif num == 4:
             canvas4 = Canvas(v1, width=200, height=200,bg='white')  # OBJETO DE LA TKINTER   CANVAS(FIGURAS)     200 pixeles de ancho 200 ancho
             puntos  = [102,201,233,134,431,331,122,134]
             canvas4.create_polygon(puntos)
             canvas4.pack(expand=YES, fill=BOTH)  # DESPLEGAR EL CANVAS, EXPAND QUE SEA EXPANDIBLE
    
        elif num == 5:
             canvas5 = Canvas(v1, width=200, height=200,bg='white')  # OBJETO DE LA TKINTER   CANVAS(FIGURAS)     200 pixeles de ancho 200 ancho
    
             canvas5.create_polygon(400,210,580,480,210,300,580,300,210,480,width=10,fill=(a[1]))
             canvas5.pack(expand=YES, fill=BOTH)  # DESPLEGAR EL CANVAS, EXPAND QUE SEA EXPANDIBLE
    
    
    #pentagono 146,0,291,106,236,277,26,277,0,106
    def ocultar(ventana): ventana.destroy()
    def ejecutar(f): v0.after(200, f)
    
    
    # V0 donde se va desplegar el boton
    b1 = Button(v0, text='Abrir ventana con linea', command=lambda: ejecutar(mostrar(1)))
    b1.grid(row=1, column=1)  # desplegar boton
    
    b2=Button(v0,text='Abrir ventana cuadro',command=lambda:ejecutar(mostrar(2)))
    b2.grid(row=1,column=2)  #desplegar boton
    
    b3=Button(v0,text='Abrir ventana circulo',command=lambda:ejecutar(mostrar(3)))
    b3.grid(row=1,column=3)  #desplegar boton
    
    b4=Button(v0,text='Abrir ventana poligono',command=lambda:ejecutar(mostrar(4)))
    b4.grid(row=1,column=4)  #desplegar boton
    
    b5=Button(v0,text='Abrir ventana poligono estrella',command=lambda:ejecutar(mostrar(5)))
    b5.grid(row=1,column=5)  #desplegar boton
    v0.mainloop()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

---
title: Chooser
date: 2020-05-07
---
Example Python program Chooser.py

## Modules

* from Tkinter import *
* import tkColorChooser #libreria para obtener la gama de colores

## Methods

* def mostrar(num):
* def ocultar(ventana):ventana.destray()
* def ejecutar(f):v0.after(200,f)

## Code

Python tkinter example

    
    1
    2
    3
    4
    5
    6
    7
    8
    9
    10
    11
    12
    13
    14
    15
    16
    17
    18
    19
    20
    21
    22
    23
    24
    25
    26
    27
    28
    29
    30
    31
    32
    33
    34
    35
    36
    37
    38
    39
    40
    41
    42
    43
    44
    45
    46
    47
    48
    49
    50
    51
    52
    53
    54
    55
    56
    57
    58
    59
    60
    61
    62
    63
    64
    65
    66
    67
    68
    69
    70
    71
    72
    73
    74
    75
    76
    77
    78
    79
    80
    81
    <span style="background-color: white;"># -*-# -*- coding: utf-8 -*-
    from Tkinter import *
    import tkColorChooser #libreria para obtener la gama de colores
     
    #crecion de la ventana principal
    v0 = Tk()
    v0.title('Ventana principal')
    v0.config(bg = 'brown') #bg para el color de fondo de la ventana
    v0.geometry('500x500')#tamaño de la ventana
    v0.iconbitmap("descarga.ico")#para cambiar el icono de la ventana
     
     
    #funciones
    def mostrar(num):
        #aparece la gamade colores RGB o en numero hexadecimal
        a=tkColorChooser.askcolor()
        #b=tkColorChooser.askcolor()
        #ventana secundaria
        v1 = Toplevel(v0)
        v1.title('ventana hija')
        v1.protocol('Wn_DELETE_WINDOW',"onexit")#para cerrar la ventana por medio de la cruz
        v1.geometry('300x300')#tamaño de la ventana
        v1.iconbitmap("vhija.ico")  # para cambiar el icono de la ventana
        #condiciones para los botones
        if num == 1:
            canvas1=Canvas(v1,width=200,height=200, bg='white')#(b[1])) esto es para seleccionar el color de fondo# OBJETO DE LA TKINTER   CANVAS(FIGURAS)     200 pixeles de ancho 200 ancho
            canvas1.pack(expand = YES, fill = BOTH)  #DESPLEGAR EL CANVAS, EXPAND QUE SEA EXPANDIBLE
            canvas1.create_line(100,200,200,100, width = 10, fill=(a[1]))#en fil añadimos (a[1]) para que se coloque el color seleccionado en el trazo
        elif num == 2:
            canvas2 = Canvas(v1, width=200, height=200,
                             bg='white')  # OBJETO DE LA TKINTER   CANVAS(FIGURAS)     200 pixeles de ancho 200 ancho
            canvas2.pack(expand=YES, fill=BOTH)  # DESPLEGAR EL CANVAS, EXPAND QUE SEA EXPANDIBLE
            canvas2.create_rectangle(10, 200, 200, 10, width=10, fill=(a[1]))
     
            # circulo
        elif num == 3:
            canvas3 = Canvas(v1, width=200, height=200,
                             bg='white')  # OBJETO DE LA TKINTER   CANVAS(FIGURAS)     200 pixeles de ancho 200 ancho
            canvas3.pack(expand=YES, fill=BOTH)  # DESPLEGAR EL CANVAS, EXPAND QUE SEA EXPANDIBLE
            canvas3.create_oval(10, 200, 200, 10, width=10, fill=(a[1]))
            # poligono
     
            elif num == 4:  #El polygono de Hugo
            canvas4 = Canvas(v1, width=200, height=200,
                             bg='white')  # OBJETO DE LA TKINTER   CANVAS(FIGURAS)     200 pixeles de ancho 200 ancho
            canvas4.pack(expand=YES, fill=BOTH)  # DESPLEGAR EL CANVAS, EXPAND QUE SEA EXPANDIBLE
            puntos = [102, 201, 233, 134, 431, 331, 122, 134]
            canvas4.create_polygon(puntos, width=10, fill=(a[1]))
     
        elif num == 5: #La estrella de zapata
            canvas5 = Canvas(v1, width=200, height=200,
                             bg='white')  # OBJETO DE LA TKINTER   CANVAS(FIGURAS)     200 pixeles de ancho 200 ancho
            canvas5.pack(expand=YES, fill=BOTH)  # DESPLEGAR EL CANVAS, EXPAND QUE SEA EXPANDIBLE
            puntos = [10,40,40,40,50,10,60,40,90,40,65,60,75,90,50,70,25,90,35,60]
            canvas5.create_polygon(puntos, width=10, fill=(a[1]))
     
    def ocultar(ventana):ventana.destray()
    def ejecutar(f):v0.after(200,f)
     
     
     
    #botones
    # V0 donde se va desplegar el boton
    b1 = Button(v0, text='Abrir ventana con linea', command=lambda: ejecutar(mostrar(1)))
    b1.grid(row=1, column=1)  # desplegar boton
     
    b2=Button(v0,text='Abrir ventana cuadro',command=lambda:ejecutar(mostrar(2)))
    b2.grid(row=1,column=2)  #desplegar boton
     
    b3=Button(v0,text='Abrir ventana circulo',command=lambda:ejecutar(mostrar(3)))
    b3.grid(row=1,column=3)  #desplegar boton
     
    b4=Button(v0,text='Abrir ventana poligono',command=lambda:ejecutar(mostrar(4)))
    b4.grid(row=1,column=4)  #desplegar boton
     
    b5=Button(v0,text='Abrir ventana poligono',command=lambda:ejecutar(mostrar(5)))
    b5.grid(row=1,column=5)  #desplegar boton
     
    v0.mainloop()
     
    </span>

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

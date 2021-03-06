---
title: Filtro
date: 2020-05-07
---
Example Python program Filtro.py
For Python version 2.x.
To test your Python version use:

    python --version

## Modules

* import Tkinter
* import Image, ImageTk
* from sys import argv
* import math

## Methods

* def b_and_w(scale):
* def grayscale(tipo):
* def blur(maxiter, normalizado):
* def color_blur(maxiter):
* def getcolor(color):
* def color_inv():

## Code

Python tkinter example

    import Tkinter
    import Image, ImageTk
    from sys import argv
    import math
    
    file = argv[1]
    
    im = Image.open(file).convert("RGB")
    original = im
    (x,y) = im.size
    
    def b_and_w(scale):
        grayscale("prom")
        for i in range(x):
            for j in range(y):
                pixel = im.getpixel((i,j))[0]
                if(pixel<scale):
                    pixel = 0
                else:
                    pixel = 255
                im.putpixel((i,j), (pixel,pixel,pixel))
    
    def grayscale(tipo):
        for i in range(x):
            for j in range(y):
                (r,g,b)=original.getpixel((i, j))
                if tipo == "min":
                    gray = min((r,g,b))
                if tipo == "max":
                    gray = max((r,g,b))
                if tipo == "r":
                    gray = r
                if tipo == "g":
                    gray = g
                if tipo == "b":
                    gray = b
                if tipo == "prom":
                    gray = (r+g+b)/3
                im.putpixel((i,j), (gray,gray,gray))
    
    def blur(maxiter, normalizado):
        grayscale("prom")
        iter = 0
        while iter < maxiter:
            print "Iteracion: ", iter
            for i in range(x):
                for j in range(y):
                    prom = []
                    k=0
                    pixel=im.getpixel((i, j))[0]
                    if(i-1>=0):
                        prom.append(im.getpixel((i-1, j))[0])
                        k+=1
                    if(i+1<x):
                        prom.append(im.getpixel((i+1, j))[0])
                        k+=1
                    if(j+1<y):
                        prom.append(im.getpixel((i, j+1))[0])
                        k+=1
                    if(j-1>=0):
                        prom.append(im.getpixel((i, j-1))[0])
                        k+=1
                    promedio = 0;
                    for valor in prom:
                        promedio+=valor
                    promedio=promedio/k
                    im.putpixel((i,j), (promedio,promedio,promedio))            
            iter+=1
    
    def color_blur(maxiter):
        iter = 0
        while iter < maxiter:
            for i in range(x):
                for j in range(y):
                    promr = []
                    promg = []
                    promb = []
                    k=0
                    (r,g,b)=original.getpixel((i, j))
                    if(i-1>=0):
                        (rn,gn,bn)=original.getpixel((i-1, j))
                        promr.append(rn)
                        promg.append(gn)
                        promb.append(bn)
                        k+=1
                    if(i+1<x):
                        (rs,gs,bs)=original.getpixel((i+1, j))
                        promr.append(rs)
                        promg.append(gs)
                        promb.append(bs)
                        k+=1
                    if(j+1<y):
                        (re,ge,be)=original.getpixel((i, j+1))
                        promr.append(re)
                        promg.append(ge)
                        promb.append(be)
                        k+=1
                    if(j-1>=0):
                        (ro,go,bo)=original.getpixel((i, j-1))
                        promr.append(ro)
                        promg.append(go)
                        promb.append(bo)
                        k+=1
                    promedior = 0
                    promediog = 0
                    promediob = 0
                    for valor in promr:
                        promedior+=valor
                    for valor in promg:
                        promediog+=valor
                    for valor in promb:
                        promediob+=valor
                    promedior=promedior/k
                    promediog=promediog/k
                    promediob=promediob/k
                    im.putpixel((i,j), (promedior,promediog,promediob))
            iter+=1
    
    def getcolor(color):
        for i in range(x):
            for j in range(y):
                (r,g,b)=original.getpixel((i,j))
                if(color=="r" or color=="R"):
                    im.putpixel((i,j),(r,0,0))
                if(color=="g" or color =="G"):
                    im.putpixel((i,j),(0,g,0))
                if(color=="b" or color == "B"):
                    im.putpixel((i,j),(0,0,b))
    
    def color_inv():
        for i in range(x):
            for j in range(y):
                (r,g,b)=original.getpixel((i,j))
                im.putpixel((i,j),(255-r,255-g,255-b))
    
    if(argv[2]=="INV" or argv[2]=="inv"):
            color_inv()
            im.save("INV_"+file)
            
    if(argv[2]=="GC" or argv[2]=="gc"):
        if(len(argv)==4):
            getcolor(argv[3])
            im.save("GC_"+file)
        else:
            print "Introduzca 'r', 'g' o 'b' segun el color que desee extraer."
            
    if(argv[2]=="BW" or argv[2]=="bw"):
        if(len(argv)==4):
            b_and_w(int(argv[3]))
            im.save("BW_"+file)
        else:
            print "Introduzca la escala de blanco y negro como parametro."
            
    if(argv[2]=="G" or argv[2]=="g"):
        if(len(argv)==4):
            grayscale(argv[3])
            im.save("G_"+file)
        else:
            print "Introduzca el tipo de escala de gris (min, max, r, g, b, prom)."
            
    if(argv[2]=="B" or argv[2]=="b"):
        if(len(argv)==4):
            blur(int(argv[3]), False)
            im.save("B_"+file)
        else:
            print "Introduzca el numero de iteraciones de blur como parametro."
            
    if(argv[2]=="CB" or argv[2]=="cb"):
        if(len(argv)==4):
            color_blur(int(argv[3]))
            im.save("CB_"+file)
        else:
            print "Introduzca el numero de iteraciones de blur como parametro."
            
    ventana = Tkinter.Tk()
    im2 = ImageTk.PhotoImage(im)
    Tkinter.Label(ventana, image=im2).pack()
    
    ventana.mainloop()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

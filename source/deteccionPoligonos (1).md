---
title: deteccionPoligonos (1)
date: 2020-05-07
---
Example Python program deteccionPoligonos (1).py
For Python version 2.x.
To test your Python version use:

    python --version

## Modules

* import operator
* import numpy as np
* import random
* from math import atan2, sin, cos, pi, sqrt
* import Tkinter
* from PIL import ImageDraw
* import Image
* import ImageTk
* from sys import argv
* import time

## Methods

* def convolucion(imagen, h):
* def filtro(original):
* def filtroPorNumeros(im,n):
* def escalaDeGrises(im):
* def nuevaImagen(matriz):
* def binarizacion(imagen):
* def deteccionLinea(g, gx, gy, imagen, prop):
* def main():

## Code

Python tkinter example

    import operator
    import numpy as np
    import random
    from math import atan2, sin, cos, pi, sqrt
    import Tkinter
    from PIL import ImageDraw
    import Image
    import ImageTk
    from sys import argv
    import time
    
    def convolucion(imagen, h):
        iwidth, iheight = imagen.size
        imagen = imagen.convert('L')
        im = imagen.load()
        mheight, mwidth = h.shape
        print "Imagen size: ",imagen.size
        print "H: ",h.shape
        g = np.zeros(shape=(iheight, iwidth))
        for x in xrange(iheight):
            for y in xrange(iwidth):
                sum = 0.0
                for j in xrange(mheight):
                    zj = ( j - ( mheight / 2 ) )
                    for i in xrange(mwidth):
                        zi = ( i - ( mwidth / 2 ) )
                        try:
                            sum += im[y + zi, x + zj] * h[i,j]
                        except:
                            pass
                print x, y
                g[x,y] = sum
        print "Convolucion"
        print g
        return g
    
    def filtro(original):
        width, height = original.size
        print width, height
        original = original.convert('L')
        modificado = Image.new(mode='L', size =(width,height))
        org = original.load()
        mod = modificado.load()
        contador = 0
        min = 0
        max = 0
        for y in xrange(height):
            for x in xrange(width):
                pixel = org[x,y]
                if min >= pixel:
                    min = pixel
                if max <= pixel:
                    max = pixel
        print "MAX:",max," MIN:",min
        for y in xrange(height):
            for x in xrange(width):
                pixel = org[x,y]
                try:
                    pixel += org[x-1,y]
                    contador+=1
                except:
                    None
                try:
                    pixel += org[x+1,y]
                    contador+=1
                except:
                    None
                try:
                    pixel += org[x,y+1]
                    contador+=1
                except:
                    None
                try:
                    pixel += org[x,y-1]
                    contador+=1
                except:
                    None
                promedio = (pixel) / (contador)
                r = max - min
                prop = 256.0 / r
                p = int((promedio -min) * prop)
                if p <= 90:
                    mod[x,y] = 0
                else: 
                    mod[x,y] = 255
                print mod[x,y]
                print x,y
                contador = 1
                pixel = 0
        data = np.array(modificado)
        print data
        print data.shape
        im = Image.fromarray(data)
        return im
             
    def filtroPorNumeros(im,n):
        for x in xrange(n):
            im = filtro(im)
        return im
    
    def escalaDeGrises(im):
        width, height = im.size
        print width, height
        im = im.convert('RGB')
        pix = im.load()
        promedio = 0.0
        for y in xrange(height):
                for x in xrange(width):
                    r, g, b = pix[x, y]
                    promedio = (r+g+b)/3.0
                    pix[x, y] = int(promedio), int(promedio), int(promedio)
        data = np.array(im)
        im2 = Image.fromarray(data)
        return im2
    
    def nuevaImagen(matriz):
        height, width = matriz.shape
        print matriz.shape
        imagen = Image.new(mode='L', size =(width,height))
        im = imagen.load()
        print imagen.size
        for x in xrange(height):
            for y in xrange(width):
                im[y, x] = matriz[x, y]
        data = np.array(imagen)
        print data
        im = Image.fromarray(data)
        return im
    
    def binarizacion(imagen):
        width, height = imagen.size
        imagen = imagen.convert('L')
        im = imagen.load()
        for x in xrange(height):
            for y in xrange(width):
                pixel = im[y, x]
                if pixel < 3:
                    im[y, x] = 0
                else:
                    im[y, x] = 255
        data = np.array(imagen)
        im = Image.fromarray(data)
        return im
    
    def deteccionLinea(g, gx, gy, imagen, prop):
        width, height = imagen.size
        imagen = imagen.convert('RGB')
        im = imagen.load()
        freq = dict()
        a = list()
        for x in xrange(height):
            for y in xrange(width):
                print "Este es x: ",x," este es y: ",y
                theta = atan2(gx[x,y],gy[x,y])
                g = sqrt(gx[x, y]**2 + gy[x, y]**2)
                print "G:",g
                if g > 0 or g < -0.000001:
                    a.append((x,y,theta))
                print "Valor gx[%s,%s] : %s"%( x, y, gx[x,y])
                print "Valor gy[%s,%s] : %s"%( x, y, gy[x,y])
                p = ( x * cos( theta ) ) + ( y * sin( theta ) )
                key = "%.2f %.0f"%(theta, p)
                print "theta: ",theta," p: ",p
                if key in freq:
                    freq["%.2f %.0f"%(theta, p)] += 1
                else:
                    freq["%.2f %.0f"%(theta, p)] = 1
        freq_f = dict()
        freq = sorted(freq.iteritems(), key=operator.itemgetter(1))
        print freq
        print freq[0][0]
        print freq[0][1]
        k = int(len(freq) * prop)
        for f in freq:
            if len(freq_f) <= k:
                freq_f[f[0]] = f[1]
        for x in xrange(height):
            for y in xrange(width):
                theta = atan2(gy[x,y],gx[x,y])
                p = ( x * cos( theta ) ) + ( y * sin( theta ) )
                key = "%.2f %.0f"%(theta, p)
                if key in freq_f:
                    im[y, x] = 0,255,0
        print "gx: ",gx.shape
        print "gx matriz: ",gx
        print "gy: ",gy.shape
        print "gy matriz: ",gy
        print "Frecuencias: ",sorted(freq_f.iteritems(), key=operator.itemgetter(1))
        data = np.array(imagen)
        im = Image.fromarray(data)
        return im, a
    
    def main():
        imagen = Image.open(argv[1])
        original = imagen
        escalaGrises = escalaDeGrises(imagen)
        px = np.array([[-1,0,1], [-1,0,1], [-1,0,1]])
        py = np.array([[1,1,1], [0,0,0], [-1,-1,-1]])
        t1 = time.time()
        gx = convolucion(escalaGrises, px)
        gy = convolucion(escalaGrises, py)
        gx_2 = gx ** 2
        gy_2 = gy ** 2
        g = (gx_2 + gy_2 ) ** 1.0/2.0
        print g
        min = np.min(g)
        max = np.max(g)
        h, w = g.shape
        minimos = np.ones(shape=(h, w))
        minimos *= min
        g = g - min
        print "Restando el minimo", g
        g = g / (max - min)
        print "Dividiendo el max-min",g
        print "Max: ",np.max(g)," Min: ",np.min(g)
        bn = np.ones(shape=(h, w))
        bn *= 255
        g = g * bn
        print "Max: ",np.max(g)," Min: ",np.min(g)
        imagen_nueva = nuevaImagen(g)
        #imagen_binaria = binarizacion(imagen_nueva)
        imagen_lineas, a = deteccionLinea(g, gx, gy, imagen_nueva, float(argv[2]))
        print "lista : ",a
        root = Tkinter.Tk()
        tkimageLineas = ImageTk.PhotoImage(imagen_lineas)
        Tkinter.Label(root, image = tkimageLineas).pack(side="left")
        #Tkinter.Label(root, image = tkimageConvexHull).pack(side="top")
        t2 =time.time()
        print "Tiempo total: ",t2-t1
        root.mainloop()
    main()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

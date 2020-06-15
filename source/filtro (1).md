---
title: filtro (1)
date: 2020-05-07
---
Example Python program filtro (1).py

## Modules

* import numpy as np
* import Tkinter
* from PIL import ImageDraw
* import Image
* import ImageTk
* from sys import argv

## Methods

* def filtro(original):
* def filtroPorNumeros(im,n):
* def escalaDeGrises(im):
* def main():

## Code

Python tkinter example

    import numpy as np
    import Tkinter
    from PIL import ImageDraw
    import Image
    import ImageTk
    from sys import argv
    
    def filtro(original):
        width, height = original.size
        print width, height
        original = original.convert('L')
        modificado = Image.new(mode='L', size =(width,height))
        org = original.load()
        mod = modificado.load()
        contador = 0
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
                promedio = (pixel)/ (contador)
                mod[x,y] = int(promedio) 
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
    
    def main():
        imagen = Image.open(argv[1])
        original = imagen
        escalaGrises = escalaDeGrises(imagen)
        modificado = filtroPorNumeros(escalaGrises, int(argv[2]))
        root = Tkinter.Tk()
        tkimageModf = ImageTk.PhotoImage(modificado)
        tkimageOrig = ImageTk.PhotoImage(original)
        Tkinter.Label(root, image = tkimageModf).pack()
        Tkinter.Label(root, image = tkimageOrig).pack()
        root.mainloop()
    main()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

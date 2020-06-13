---
title: agujeros
date: 2020-05-07
---
Example Python program agujeros.py

## Modules

* from sys import argv
* from math import fabs, pow, sqrt
* import Image, ImageDraw
* #import ImageOps
* import Tkinter

## Methods

* def function():
* def filtro(image):
* def greyscale(image):
* def hist_hor(image, salida = "histograma horizontal.txt"):
* def hist_ver(image, salida = "histograma vertical.txt"):
* def encontramos(hist):
* def deteccion(ima, size=(150, 150)):
* def main():

## Code

Python tkinter example

    #!/usr/bin/python
    
    from sys import argv
    from math import fabs, pow, sqrt
    import Image, ImageDraw
    #import ImageOps
    import Tkinter
    
    def function():
    	root = Tkinter.Tk()
    	root.title("Rellenar Elipses")
    	tkimage = ImageTk.PhotoImage(imagen)
    	Tkinter.Label(root, image = tkimage).pack()
    	root.mainloop() 
    
    def filtro(image):
        imagen = image.load()
        copiar = (image.copy()).load()
        for i in range(image.size[0]):
            for j in range(image.size[1]):
                t = []
                for h in range(i-1, i+2):
                    for l in range(j-1, j+2):
                        if h >= 0 and l >= 0 and h < image.size[0] and l < image.size[1]:
                            t.append(copiar[h, l])
                t.sort()
                imagen[i,j] = int(t[int(len(t)/2)])
        return imagen
    
    ####
    def greyscale(image):
    	imagen = image.load()
    	x,y = imagen.size
    	for i in range(x):
    		for j in range(y):
    			(r,g,b) = pixeles[i,j]
    			gris = (r+g+b)/3
    			pixeles[i,j]=(gris,gris,gris)
    	return imagen 	
    ###
    	
    def hist_hor(image, salida = "histograma horizontal.txt"):
        hist = list()
        imagen = image.load()
        file = open(salida, "w")
        for x in range(image.size[0]):
            suma = 0
            for y in range(image.size[1]):
                suma += imagen[x, y]
            file.write(str(x)+" "+str(suma)+"\n")
            hist.append(suma)
        file.close()
        return hist
     
    def hist_ver(image, salida = "histograma vertical.txt"):
        hist = list()
        imagen = image.load()
        file = open(salida, "w")
        for y in range(image.size[1]):
            suma = 0
            for x in range(image.size[0]):
                suma += imagen[x, y]
            file.write(str(y)+" "+str(suma)+"\n")
            hist.append(suma)
        file.close()
        return hist
    
    def encontramos(hist):
        for i in range(1, len(hist)-1):
            if hist[i-1] > hist[i] and hist[i+1] > hist[i]:
                yield i
    
    #Detectamos la linea y dibujamos			
    def deteccion(ima, size=(150, 150)):
        image = Image.open(ima)
        original = image.copy()
        image.thumbnail(size, Image.BILINEAR)
    	
        #image = ImageOps.grayscale(image)
        filtro(image)
     
        horizontal_hist = hist_hor(image)
        vertical_hist = hist_ver(image)
        
        h = [y for y in encontramos(horizontal_hist)]
        v = [x for x in encontramos(vertical_hist)] 
     
        cosa = image.size
        image = original
        cosa = (float(image.size[0])/cosa[0], float(image.size[1])/cosa[1])
        
    	draw = ImageDraw.Draw(image)
        
        for x in h:
            x = int(x*cosa[0])
            draw.line((x, 0, x, image.size[1]), fill=(255, 0, 0))
     
        for y in v:
            y = int(y*cosa[1])
            draw.line((0, y, image.size[0], y), fill=(0, 0, 0))
    
    	image.save("salida_detecado.png")
     
    def main():
    	#function()
        deteccion(argv[1])
     
    main()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

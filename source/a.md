---
title: a
date: 2020-05-07
---
Example Python program a.py

## Modules

* import sys
* import pygame 
* import Tkinter
* from PIL import Image, ImageTk

## Methods

* def neighbor():
* def umbral():
* def gray_scale():
* def main():

## Code

Python tkinter example

    import sys
    import pygame 
    import Tkinter
    
    from PIL import Image, ImageTk
    
    root = Tkinter.Tk()
    
    image = sys.argv[ 1 ]
    
    im = Image.open( image )
    pix = im.load()
    w, h = im.size
    
    def neighbor():
        
        # Numero de iteraciones deseadas
        num_iter = int( raw_input( "Numer de iteraciones: " ) )
            
        for l in range( num_iter ):
    
            # Recorrido de pixeles
            for i in range( w ):
                for j in range( h ):
                    
                    # aux es la variable con la que se sabe en cuanto dividirlo
                    # color es la suma RGB de cada pixel vecino y el de la posicion actual
                    aux = 1
                    color = 0
                    
                    # Toma el RGB del pixel
                    r, g, b = pix[ i, j ]
    
                    color += ( r + g + b ) / 3
                    
                    # Vecino Norte
                    if i - 1 < 0:
                        None
                    else:
                        r1, g1, b1 = pix[ ( i - 1 ), j ]
                        color += ( r1 + g1 + b1 ) / 3 
                        aux = aux + 1
                        
                    # Vecino Sur
                    if i + 1 >= w:
                        None
                    else:
                        r2, g2, b2 = pix[ ( i + 1 ), j ]
                        color += ( r2 + g2 + b2 ) / 3
                        aux = aux + 1
                    
                    # Vecino Oeste
                    if j - 1 < 0:
                        None
                    else:
                        r3, g3, b3 = pix[ i, ( j - 1 ) ]
                        color += ( r3 + g3 + b3 ) / 3
                        aux = aux + 1
                    
                    # Vecino Este
                    if j + 1 >= h:
                        None
                    else:
                        r4, g4, b4 = pix[ i, ( j + 1 ) ]
                        color += ( r4 + g4 + b4 ) / 3
                        aux = aux + 1
                
                    color /=  aux
                    
                    # Coloca el valor obtenido en el pixel actual
                    pix[ i, j ] = ( color, color, color )
    
        im.show()
    
    def umbral():
    
        # Umbral para binarizarla
        u = int( raw_input( "Numero: " ) )
    
        for i in range( w ):
            for j in range( h ):
    
                r, g, b = pix[ i, j ]
                
                gray = int(  ( r + g + b ) / 3 )
                
                if gray < u:
                    pix[ i, j ] = ( 0, 0, 0 )
    
                else:
                    pix[ i, j ] = ( 255, 255, 255 )
                    
        im.show()
    
    def gray_scale():
    
        # Recorrido de pixles
        for i in range( w ):
            for j in range( h ):
                r, g, b = pix[ i, j ]
    
                gray = int(  ( r + g + b ) / 3 )
                
                pix[ i, j ] = ( gray, gray, gray )
    
        im.show()
    
    def main():
        
        tkIm = ImageTk.PhotoImage( im )
    
        # Ventana principal donde se muestra la imagen original
        window = Tkinter.Label( root, image = tkIm ).pack()
    
        # Opciones de convertimiento
        g = Tkinter.Button( root, text = "Escala de grises", command = gray_scale ).pack()
        u = Tkinter.Button( root, text = "Umbral", command = umbral ).pack()
        n = Tkinter.Button( root, text = 'Vecinos', command = neighbor ).pack()
    
        root.mainloop()    
    
    main()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

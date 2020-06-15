---
title: escribir
date: 2020-05-07
---
Example Python program escribir.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import os

## Methods

* def leer():
* def main():

## Code

Python example

    #!/usr/bin/env python
    # -*- coding: utf-8 -*-
    
    import os
    
    PATH = "datos.csv"
    
    def leer():
        global PATH
        datos_csv = open(PATH,"r")
        print("#Contenido:")
        print(datos_csv.read())
        datos_csv.close()
    
    
    def main():
        global PATH
        datos_csv = None
        try:
            #se usa 'w' para sobre escribir el contenido del archivo
            datos_csv = open(PATH,"w")
            if os.path.isfile(PATH) == True:
                print("El archivo existe.")
            datos_csv.write("Nombre, Color, Precio\n")
            datos_csv.write("Manzana, Rojo, 12.03\n")
            datos_csv.write("Pera, Verde, 9.88\n")
        except FileNotFoundError as e:
            print("El archivo no existe:",e)
        finally:
            print("Archivo sobrescrito.\nCerramos el archivo.")
            datos_csv.close()
    
        leer()
        #se usa 'a' para añadir sin borrar
        datos_csv = open(PATH,'a')
        datos_csv.write("Platano, Amarillo,14.6\n")
        datos_csv.close()
        leer()
    
    
    if __name__ == '__main__':
        main()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

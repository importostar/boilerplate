---
title: lectura
date: 2020-05-07
---
Example Python program lectura.py
Python version 3.x or newer.
To check the Python version use:

    python --version


## Methods

* def main():

## Code

Python example

    #!/usr/bin/env python
    # -*- coding: utf-8 -*-
    
    PATH = "datos.csv"
    
    def main():
        global PATH
        datos_csv = None
        # 1era forma
        try:
            datos_csv = open(PATH,"r")
            print("Contenido:\n",datos_csv.read())
        except FileNotFoundError as noexiste:
            print("El archivo no existe:",noexiste)
        finally:
            datos_csv.close()
    
        print("\n")
        # 2da forma
        try:
            datos_csv = open(PATH,"r")
            print("Contenido:")
            with  datos_csv as fichero:
                for linea in fichero:
                    print(linea)
        except FileNotFoundError as noexiste:
            print("El archivo no existe:",noexiste)
        finally:
            datos_csv.close()
    
        # 3era forma
        print("\n")
        try:
            datos_csv = open(PATH,"r")
            #Sólo lee la 1era línea
            print("Contenido de la primera línea: ",datos_csv.readline())
            #Leer varias líneas
            print("Contenido por línea: ",datos_csv.readlines())
            #Usando un for
    
        except FileNotFoundError as noexiste:
            print("El archivo no existe:",noexiste)
        finally:
            datos_csv.close()
    
        #4ta forma
        print("\n")
        try:
            datos_csv = open(PATH,"r")
            for dato in datos_csv:
                print(dato)
        except IOError as error:
            print("Ha ocurrido un error:"+error)
        finally:
            datos_csv.close()
    
    
    if __name__ == '__main__':
        main()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

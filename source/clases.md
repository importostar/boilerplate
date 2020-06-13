---
title: clases
date: 2020-05-07
---
Example Python program clases.py
Python version 3.x or newer.
To check the Python version use:

    python --version


## Classes

* class Datos(object):
* class Extractor:
* class Figura(object):
* class Triangulo(Figura):
* class Rectangulo(Figura):
* class Nodo(object):

## Methods

* def __init__(self,nombre,apellidos,correo,fecha):
* def __str__(self):
* def __init__(self):
* def __str__(self):
* def __init__(self):
* def __init__(self):
* def __init__(self):
* def __init__(self):
* def __init__(self,nodo, valor):
* def __str__(self):

## Code

Python example

    #!/usr/bin/env python
    # -*- coding: utf-8 -*-
    
    
    class Datos(object):
        def __init__(self,nombre,apellidos,correo,fecha):
            self.nombre=nombre
            self.apellidos=apellidos
            self.correo=correo
            self.fecha=fecha
    
        def __str__(self):
            return "Datos{nombre:"+self.nombre+",apellidos:"+self.apellidos+",correo:"+self.correo+",fecha:"+str(self.fecha)+"}"
            
    
    class Extractor:
        ruta = ''
    
        def __init__(self):
            print("objeto Extractor creado e inicializado")
    
        def __str__(self):
            return "Extrator{ruta:"+self.ruta+"}"
    
    
    class Figura(object):
        alto=0.0
        ancho=0.0
        def __init__(self):
            print("Objeto Figura creado e inicializado")
    
    class Triangulo(Figura):
        tipo = ''
        def __init__(self):
            print("Objeto Triangulo creado e inicializado")
    
    
    class Rectangulo(Figura):
        def __init__(self):
            print("Objeto Rectangulo creado e inicalizado")
    
    
    class Nodo(object):
        nodo = None
        valor = ''
    
        def __init__(self):
            print("objeto Nodo creado e inicializado")
    
        def __init__(self,nodo, valor):
            self.nodo=nodo
            self.valor=valor
            print("objeto Nodo creado e inicializado")
    
        def __str__(self):
            return "Nodo{nodo:"+str(self.nodo)+", valor:"+self.valor+"}"

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

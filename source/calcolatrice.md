---
title: calcolatrice
date: 2020-05-07
---
Example Python program calcolatrice.py
For Python version 2.x.
To test your Python version use:

    python --version


## Methods

* def somma(a,b):
* def moltiplicazione(a,b):
* def divisione(a,b):
* def sottrazione(a,b):

## Code

Python example

    # -*- coding:utf-8 -*-
    
    def somma(a,b):
        return a+b
    
    def moltiplicazione(a,b):
        return a*b
    
    def divisione(a,b):
        return a/b
    
    def sottrazione(a,b):
        return a-b
    
    
    while True:
        
        print "Benvenuti nel programma calcolatrice"
        print "===================================="
        print "Operazioni disponibili:"
        print "1) Somma"
        print "2) Moltiplicazioni"
        print "3) Divisione"
        print "4) Sottrazione"
        print "------------------------------------"
        print "0) Esci"
        scelta = input("Inserire una scelta valida: ")
        if scelta == 0:
            break
        if scelta not in [1,2,3,4]:
            print "Scelta non valida"
            continue
        a = input("Primo operando: ")
        b = input("Secondo operando: ")
        if scelta == 1:
            print "La somma e' ", somma(a,b)
        elif scelta == 2:
            print "La moltiplicazione e' ", moltiplicazione(a,b)
        elif scelta == 3:
            print "la divisione e' ", divisione(a,b)
        elif scelta == 4:
            print "la sottrazione e' ", sottrazione(a,b)
    
    print "\nGrazie e alla prossima!!!"
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

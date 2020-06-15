---
title: archipi
date: 2020-05-07
---
Example Python program archipi.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* from tkinter.messagebox import *
* from tkinter import *
* import math

## Methods

* def valid(win, n):
* def show():
* def archimede(n):

## Code

Python tkinter example

    from tkinter.messagebox import *
    from tkinter import *
    import math
    
    def valid(win, n):
        """
        Affiche une boite de dialogue informative communiquant le résulat
        win: fenetre tkinter
        n: nombre d'itérations
        Retourne None
        """
        vn = int(n)
        result = archimede(vn)
        ncot = 4*2**vn
        showinfo("Résultat", "PI = {r} ; avec un ncot = {ncot}".format(r=result, ncot=ncot))
    
    def show():
        """
        Créé la boite de dialogue et l'affiche
        Retourne None
        """
        win = Tk()
        label = Label(win, text="Nombre d'itérations (sachant que nb. cotés = 4*2^n)")
        label.pack()
        value = StringVar()
        entry = Entry(win, textvariable=value, width=30)
        entry.pack()
        button = Button(win, text="Valider", command=lambda: valid(win, value.get()))
        button.pack()
        win.mainloop()
    
    def archimede(n):
        """
        Calcule PI avec la méthode d'Archimède
        n: nombre d'itérations, polygone de 4*2**n côté inscrit dans un cercle de 1 de rayon
        Retourne la valeur approchée de PI (float).
        """
        poly_cot = 2.0
        ncot = 4
        for i in range(n):
            poly_cot = 2 - 2 * math.sqrt(1 - poly_cot / 4)
            ncot *= 2
        print("ncot=", ncot)
        return ncot * math.sqrt(poly_cot) / 2
    
    show()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

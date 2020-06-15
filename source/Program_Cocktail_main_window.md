---
title: Program_Cocktail_main_window
date: 2020-05-07
---
Example Python program Program_Cocktail_main_window.py

## Modules

* import tkinter
* import getraenke_verwaltung

## Methods

* def ende():
* def glas_ok():
* def getr_verw():
* def anzeigen(self):
* #def reset():

## Code

Python tkinter example

    ###############################################
    # Erstellung der GUI zur Nutzung der Maschine #
    ###############################################
    
    import tkinter
    
    # Anfangswerte fesstlegen
    glasG = 300
    
    # Funktionen erstellen
    def ende():
        main.destroy()
    
    def glas_ok():
        glasG = str(Eglas.get())
    
    def getr_verw():
        import getraenke_verwaltung
    
    def anzeigen(self):
        lb1["text"] = "Füllmenge: " + str(getrwert1.get()) + " ml"
        lb2["text"] = "Füllmenge: " + str(getrwert2.get()) + " ml"
    
    #def reset():
        # ...
    
    # Hauptfenster erstellen
    main = tkinter.Tk()
    
    # Menüleiste erstellen und hinzufügen
    # Menü "Datei"
    mBar = tkinter.Menu(main)
    mFile = tkinter.Menu(mBar)
    mFile["tearoff"] = 0 # Menü nicht abtrennbar
    mFile.add_command(label="Reset")
    mFile.add_separator()
    mFile.add_command(label="Beenden", command=ende)
    mBar.add_cascade(label="Datei",menu=mFile)
    
    # Menü "Datenbanken"
    mDB = tkinter.Menu(mBar)
    mDB["tearoff"]=0 # Menü nicht abtrennbar
    mDB.add_command(label="Cocktails")
    mDB.add_separator()
    mDB.add_command(label="Getränke",command=getr_verw)
    mBar.add_cascade(label="Datenbanken",menu=mDB)
    
    main["menu"] = mBar
    
    ###########################################################
    # Row 0
    # Glasgröße abfragen
    # Anzeigelabel
    lbg=tkinter.Label(main,text="Glasgröße: ",width=25)
    lbg.grid(row=0, column=0, columnspan=1, sticky="we")
    Eglas = tkinter.Entry(main)
    Eglas.grid(row=0, column=1, columnspan=1, sticky="we")
    Bglas = tkinter.Button(main, text="Ok", command=glas_ok)
    Bglas.grid(row=0, column=2, columnspan=1, sticky="we")
    
    # Row 1
    # Schieberegler erstellen
    # Anzeigelabel
    lb1=tkinter.Label(main,text="Füllmenge: 0 ml",width=25)
    lb1.grid(row=1, column=0, columnspan=1, sticky="we")
    # Widget Variablen erstellen
    getrwert1 = tkinter.IntVar()
    getrwert1.set(0)
    # Scale Widget
    getr1 = tkinter.Scale(main, width=20, length=200, orient="horizontal", from_=0, to=glasG, resolution=10, tickinterval=200, command=anzeigen, variable=getrwert1)
    getr1.grid(row=1, column=1, columnspan=3)
    
    # Row 2
    # Schieberegler erstellen
    # Anzeigelabel
    lb2=tkinter.Label(main,text="Füllmenge: 0 ml",width=25)
    lb2.grid(row=2, column=0, columnspan=1, sticky="we")
    # Widget Variablen erstellen
    getrwert2 = tkinter.IntVar()
    getrwert2.set(0)
    # Scale Widget
    getr2 = tkinter.Scale(main,width=20, length=200, orient="horizontal", from_=0, to=glasG,resolution=10, tickinterval=200, command=anzeigen, variable=getrwert2)
    getr2.grid(row=2, column=1, columnspan=3)
    
    #############################################################
    main.mainloop()
    
    
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

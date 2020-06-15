---
title: basilWorldLauncher
date: 2020-05-07
---
Example Python program basilWorldLauncher.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import os
* import sys
* import time
* import tkinter as tk
* from tkinter import ttk
* from tkinter import messagebox
* from tkinter.constants import *

## Classes

* class Application(ttk.Frame):

## Methods

* def __init__(self, master=None):
* def setStyle(self):
* def createWidgets(self):
* def makeEntry(self, parent, n):
* def start(self):
* def setDoubleVars(self):
* def useLastVars(self):
* def revertToDefault(self):

## Code

Python tkinter example

    #!/usr/bin/env python3
    import os
    import sys
    import time
    import tkinter as tk
    from tkinter import ttk
    from tkinter import messagebox
    from tkinter.constants import *
    
    # try Scale Widget http://effbot.org/tkinterbook/scale.htm
    
    
    class Application(ttk.Frame):
        def __init__(self, master=None):
            ttk.Frame.__init__(self, master)
            # Il frame è gestito da pack(), contiene un widgetsFrame gestito
            # internamente da grid() e un buttonFrame che contiene solo il
            # button "Inizia" gestito da pack()
    
            # widgetsFrame ha un padding=5 ed è definito per espandersi in
            # caso di resize prendendo lo spazio disponibile (fill=BOTH)
            # Si trova in alto (side="top"), è sticky in alto
            self.widgetsFrame = ttk.Frame(self, padding=5)
            self.widgetsFrame.pack(side="top", fill=BOTH)
            # sotto rendono la griglia gestita da grid resizable
            self.widgetsFrame.grid_columnconfigure(0, weight=1)
            self.widgetsFrame.grid_rowconfigure(0, weight=1)
            # buttonFrame è sticky in basso ed è resizable
            self.buttonFrame = ttk.Frame(self)
            self.buttonFrame.pack(side="bottom", fill=BOTH)
    
            self.setDoubleVars()
            self.useLastVars()
            self.setStyle()
            self.createWidgets()
    
        def setStyle(self):
            """Imposta stile e padding di tutti i widget sullo schermo"""
            style = ttk.Style()
            style.configure("TFrame", background=self.colors["main"])
            style.configure("TLabel", padding=6, relief="flat",
                            foreground=self.colors["text"],
                            background=self.colors["main"])
            # Dichiarando name.TLabel eredito da TLabel tutti valori e ne aggiungo
            # specifici. Viene utilizzato per l'introtext con style="Intro.TLabel"
            style.configure("Intro.TLabel", font=("Sans", "9", "bold"))
            style.configure("TEntry", padding=6, relief="flat", borderwidth=0,
                            fieldbackground=self.colors["main"],
                            foreground=self.colors["text"])
            style.configure("TButton", padding=10, relief="flat",
                            font=("Sans", "10", "bold"),
                            foreground=self.colors["text"],
                            background=self.colors["accent"])
    
        def createWidgets(self):
            """Crea tutti i widget e li mostra su schermo"""
            ttk.Label(self.widgetsFrame, text=self.text['introtext'],
                      style="Intro.TLabel").grid(row=0, columnspan=2, pady=5)
            ttk.Separator(self.widgetsFrame, orient=HORIZONTAL
                          ).grid(row=1, pady=3, columnspan=2, sticky=EW)
    
            # ########## Lista di widget ##############################
            for n in range(18):
                self.makeEntry(self.widgetsFrame, n)
            # ##################### END ################################
    
            ttk.Button(self.buttonFrame, text=self.text['start'],
                       command=self.start).pack(fill=BOTH)
            ttk.Button(self.buttonFrame, text=self.text['revertdefault'],
                       command=self.revertToDefault).pack(fill=BOTH)
    
        def makeEntry(self, parent, n):
            """Crea una label con il testo al numero n di text e una entry
            la cui variabile assegnata si trova al numero n di double_vars"""
            ttk.Label(parent, text=self.text[n]).grid(row=(n + 2), sticky=NSEW)
            ttk.Entry(parent, textvariable=self.double_vars[n]
                      ).grid(row=(n + 2), column=1, sticky=NSEW)
    
        def start(self):
            """Crea il comando da lanciare per fare partire il programma"""
            command = "./basilworld"
            try:
                for n in range(18):
                    command += " "
                    command += str(self.double_vars[n].get())
            except tk.TclError:
                # Gestisce l'errore di variabile: se non è un double ritorna errore
                # In pratica se si scrivono caratteri non numerici ritorna errore
                messagebox.showerror(self.text['error'], self.text['errormessage'])
                print(self.text['errormessage'])
    
            # Non necessario, ma utile a gestire ogni tipo di problema
            except:
                messagebox.showerror(self.text['unexpected'], sys.exc_info()[0])
                print(self.text['unexpected'] + sys.exc_info()[0])
                raise
            else:
                print(command)
                with open("basilworld.log", "a") as logfile:
                    # File di log con comando e orario in cui è stato mandato
                    logfile.write(time.strftime(
                        "\n\nComando inviato il %d-%m-%Y alle %H:%M:%S\n"))
                    logfile.write(command)
                os.system(command)
                self.quit()
    
        def setDoubleVars(self):
            """Inizializza le tk.DoubleVar assegnate ad ogni entry. Usa la lista
                initial_vars per l'inizializzazione"""
            self.double_vars = []
            for n in range(18):
                self.double_vars.append(tk.DoubleVar())
                self.double_vars[n].set(self.default_vars[n])
    
        def useLastVars(self):
            """Set the double_vars list to the last configuration used, retrieved from
            the logfile"""
            if os.path.exists("basilworld.log"):
                with open("basilworld.log", "r") as logfile:
                    lastLine = logfile.readlines()[-1]
                    for i, s in enumerate(lastLine.split(" ")[1:]):
                        try:
                            self.double_vars[i].set(float(s))
                        except tk.TclError:
                            messagebox.showerror(self.text['error'],
                                                 self.text['logfile_error'])
    
        def revertToDefault(self):
            """Reverts entries' values to default_vars"""
            for n in range(18):
                self.double_vars[n].set(self.default_vars[n])
    
        default_vars = [2000, 0, 1200, 900, 500, 100, 1000,
                        10, 1, 20, 200, 1, 50, 0.1, 12, 20, 50, 0]
    
        colors = {"main": "#3e50b4",
                  "text": "#fff",
                  "accent": "#ff3f80"}
    
        text = {"title": "BasilWorld CA Launcher",
                "introtext": "Inserisci i dati qui, \
    poi clicca su Inizia per cominciare",
                "start": "Inizia",
                "revertdefault": "Torna ai valori di default",
                "error": "Errore",
                "unexpected": "Errore inaspettato",
                "errormessage": "ValueError: inserisci solamente numeri",
                "logfile_error": "Il file di log è danneggiato. \
    Non è stato possibile recuperare tutti i dati",
    
                0: "Popolazione iniziale:",
                1: "Risorse iniziali:",
                2: "Larghezza schermo:",
                3: "Altezza schermo:",
                4: "Età massima:",
                5: "Età procreazione:",
                6: "Massa massima:",
                7: "Pasto:",
                8: "Rendimento:",
                9: "Massa alla nascita:",
                10: "Parametri iniziali  massa massima:",
                11: "Velocità in x e y:",
                12: "Massa massima risorse:",
                13: "Costante gravitazionale:",
                14: "Tempo per mangiare:",
                15: "Distanza massima tra risorse:",
                16: "Tempo minimo tra due figli:",
                17: "Biodegradabilità:"}
    
    
    root = tk.Tk()
    app = Application(master=root)
    
    # Resizable code from
    # http://stackoverflow.com/questions/17598475/resizing-window-doesnt-resize-contents-in-tkinter
    app.grid(sticky=NSEW)
    root.grid_columnconfigure(0, weight=1)
    root.grid_rowconfigure(0, weight=1)
    root.resizable(True, True)
    
    root.title(Application.text['title'])
    root.mainloop()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

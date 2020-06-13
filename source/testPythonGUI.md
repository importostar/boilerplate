---
title: testPythonGUI
date: 2020-05-07
---
Example Python program testPythonGUI.py

## Modules

* import sys
* from Tkinter import *   ## notice capitalized T in Tkinter 
* from tkinter import *   ## notice here too

## Classes

* class Interface(Frame):

## Methods

* def __init__(self, fenetre, **kwargs):
* def cliquer(self):

## Code

Python tkinter example

    import sys
    try:
        # for Python2
        from Tkinter import *   ## notice capitalized T in Tkinter 
    except ImportError:
        # for Python3
        from tkinter import *   ## notice here too
    
    main = Tk()
    main.geometry("1000x500")
    main.title("Pythéo")
    
    champ_label = Label(main, text="contenu de notre champ label")
    champ_label.pack()
    
    bouton_quitter = Button(main, text="Quitter", command=main.destroy)
    bouton_quitter.pack()
    
    var_texte = StringVar()
    ligne_texte = Entry(main, textvariable=var_texte, width=30)
    ligne_texte.pack()
    
    var_case = IntVar()
    case = Checkbutton(main, text="Ne plus poser cette question", variable=var_case)
    case.pack()
    
    var_choix = StringVar()
    
    choix_rouge = Radiobutton(main, text="Rouge", variable=var_choix, value="rouge")
    choix_vert = Radiobutton(main, text="Vert", variable=var_choix, value="vert")
    choix_bleu = Radiobutton(main, text="Bleu", variable=var_choix, value="bleu")
    
    choix_rouge.pack()
    choix_vert.pack()
    choix_bleu.pack()
    
    liste = Listbox(main)
    liste.pack()
    liste.insert(END, "Pierre")
    liste.insert(END, "Feuille")
    liste.insert(END, "Ciseau")
    
    cadre = Frame(main, width=768, height=576, borderwidth=1)
    cadre.pack(fill=BOTH)
    
    message = Label(cadre, text="Notre fenêtre")
    message.pack(side="top", fill=X)
    
    class Interface(Frame):
        
        """Notre fenêtre principale.
        Tous les widgets sont stockés comme attributs de cette fenêtre."""
        
        def __init__(self, fenetre, **kwargs):
            Frame.__init__(self, fenetre, width=768, height=576, **kwargs)
            self.pack(fill=BOTH)
            self.nb_clic = 0
            
            # Création de nos widgets
            self.message = Label(self, text="Vous n'avez pas cliqué sur le bouton.")
            self.message.pack()
            
            self.bouton_quitter = Button(self, text="Quitter", command=fenetre.destroy)
            self.bouton_quitter.pack(side="left")
            
            self.bouton_cliquer = Button(self, text="Cliquez ici", fg="red",
                    command=self.cliquer)
            self.bouton_cliquer.pack(side="right")
        
        def cliquer(self):
            """Il y a eu un clic sur le bouton.
            
            On change la valeur du label message."""
            
            self.nb_clic += 1
            self.message["text"] = "Vous avez cliqué {} fois.".format(self.nb_clic)
    
    fenetre = Tk()
    interface = Interface(fenetre)
    
    interface.mainloop()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

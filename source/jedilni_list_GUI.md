---
title: jedilni_list_GUI
date: 2020-05-07
---
Example Python program jedilni_list_GUI.py

## Modules

* import Tkinter
* import tkMessageBox

## Methods

* def main():

## Code

Python tkinter example

    # -*- coding: utf-8 -*-
    import Tkinter
    import tkMessageBox
    
    jedilni_list = {}
    
    def main():
        while True:
            tkMessageBox.showinfo("Jed:", "Prosimo vnesite ime jedi: ")
            ime_jedi = vnos_jedi.get()
    
            tkMessageBox.showinfo("Cena jedi:", "Prosimo vnesite ceno jedi: ")
            cena_jedi = vnos_cene.get()
            jedilni_list[ime_jedi] = cena_jedi
    
            tkMessageBox.showinfo("Bi želeli vnesti novo jed? (da/ne): ")
            nova_jed = vnos_nove_jedi.get()
            if nova_jed.lower() == "ne":
                break
    
            with open("jedilni_list_GUI.txt", "w") as jedilna_datoteka:
                for jed in jedilni_list:
                    jedilna_datoteka.write("%s, %s €\n" % (jed, jedilni_list[jed]))
    
            with open("jedilni_list_GUI.txt", "r") as jedilni_file:
                    menu = jedilni_file.read()
                    tkMessageBox.showinfo("Danes je na meniju: ", menu)
    
    
    glavno_okno = Tkinter.Tk()
    glavno_okno.title("Dobrodošli v program Jedilni List!")
    glavno_okno.geometry("600x400+500+300")
    
    skupina1 = Tkinter.Frame(glavno_okno)
    skupina1.pack(side=Tkinter.TOP)
    
    oznaka1 = Tkinter.Label(skupina1, text= "Prosimo vnesite današnji menu", fg="black", bg="yellow")
    oznaka1.config(font=("Consolas", 20, "bold"))
    oznaka1.pack()
    
    oznaka2 = Tkinter.Label(skupina1, text= "Prosimo vnesite jed:")
    oznaka2.config(font=("Consolas", 14, "bold"))
    oznaka2.pack()
    
    vnos_jedi = Tkinter.Entry(skupina1)
    vnos_jedi.pack()
    
    oznaka3 = Tkinter.Label(skupina1, text= "Prosimo vnesite ceno jedi:")
    oznaka3.config(font=("Consolas", 14, "bold"))
    oznaka3.pack()
    
    vnos_cene = Tkinter.Entry(skupina1)
    vnos_cene.pack()
    
    oznaka4 = Tkinter.Label(skupina1, text= "Ali želite vnesti še eno jed? da/ne")
    oznaka4.config(font=("Consolas", 14, "bold"))
    oznaka4.pack()
    
    vnos_nove_jedi = Tkinter.Entry(skupina1)
    vnos_nove_jedi.pack()
    
    gumb = Tkinter.Button(skupina1, text="Vnesi!", command=main)
    gumb.pack()
    
    glavno_okno.mainloop()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

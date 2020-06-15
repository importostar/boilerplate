---
title: LotoGUI (1)
date: 2020-05-07
---
Example Python program LotoGUI (1).py

## Modules

* import random # knjiznica za generiranje nakljucnih stevil
* import Tkinter # uvoz GUI paketa
* import tkMessageBox # uvoz paketa za okna z obvestili
* from ScrolledText import * # uvoz pakeza za tekstovno polje

## Methods

* def generateNumbers(numberOfNumbers,tex):
* def main(): # main funkcija

## Code

Python tkinter example

    #!/usr/bin/env python
    # -*- coding: utf-8 -*-
    import random # knjiznica za generiranje nakljucnih stevil
    import Tkinter # uvoz GUI paketa
    import tkMessageBox # uvoz paketa za okna z obvestili
    from ScrolledText import * # uvoz pakeza za tekstovno polje
    
    def generateNumbers(numberOfNumbers,tex):
        tex.delete('1.0',Tkinter.END) # sprazni tekstovno polje
        while True:  # preko te zanke ter try/except besedama se izognemo errorjem. Uporabnik bo enostavno moral vnesti stevilo
            try: # ce je stevilo ustrezno...
                numberOfNumbers = int(numberOfNumbers.get())  # polje za vnos stevila
                break # zapusti zanko
            except ValueError: # sicer...
                return tkMessageBox.showinfo("Uppss!", "You must input a number silly :)") # javi napako
    
        listOfNumbers = []  # seznam nakljucnih stevil, zaenkrat prazen
        while numberOfNumbers > len(listOfNumbers):  # dokler je seznam krajsi od vrednosti vnesenega stevila, ponavljaj ukaze v zanki
            found = False  # s to spremenljivko bomo opazovali ali se neko stevilo ze nahaja v nasem seznamu
            someRandom = random.randint(0, 100)  # v to spremenljivko shranimo nakljucno stevilo
            if len(listOfNumbers) == 0:  # v kolikor je seznam prazen...
                listOfNumbers.append(someRandom)  # prvo nakljucno stevilo avtomatsko shranimo vanj
            else:  # v kolikor je v seznamu ze kaksno stevilo...
                for y in listOfNumbers:  # pa se sprehodi skozi seznam...
                    if someRandom == y:  # ter primerjaj vsako vrednost z vrednostjo nakljucnega stevila
                        found = True  # ce se ujemata, spremeni to spremenljivko v true
                        break  # ter prekini sprehod po seznamu
                if found == False:  # ce stevila nismo nasli v seznamu...
                    listOfNumbers.append(someRandom)  # potem ga le temu dodamo
    
        print listOfNumbers  # izpisimo vsa stevila v seznamu (terminal)
        tex.insert(Tkinter.END, "Izbrana števila so:\n" + str(listOfNumbers)) # priprni seznam stevil v tekstovno polje
    
    def main(): # main funkcija
        window = Tkinter.Tk()  # ustvarimo okno
        window.title("Lottery")  # ga poimenujemo
        window.geometry('{}x{}'.format(400, 300))  # dolocimo velikost okna
    
        instructions = Tkinter.Label(window,
                                     text="\nPlease insert how many random numbers would you like to generate:")  # vstavimo besedilo (navodila)
        instructions.pack(pady=5)  # jih dodamo v GUI, razmik med elementi na y osi(vertikalno) naj bo 5
    
        numberOfNumbers = Tkinter.Entry(window)  # polje za vnos stevila
        numberOfNumbers.pack(pady=5)  # dodamo v GUI
    
        submit = Tkinter.Button(window, text="Submit",
                                command=lambda: generateNumbers(numberOfNumbers, tex))  # gumb, ob kliku naj se klice funkcija
        submit.pack(pady=8)  # dodamo v GUI
    
        tex = ScrolledText(window, width=400, height=50)  # textovno polje
        tex.pack(pady=8)  # dodajmo v GUI
    
        window.mainloop()  # ukaz za izvajanje GUI
    
    if __name__ == "__main__":
        main() # naj se izvaja main funkcija

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

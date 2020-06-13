---
title: FizzBuzzGUI
date: 2020-05-07
---
Example Python program FizzBuzzGUI.py

## Modules

* import random
* import Tkinter # uvoz GUI paketa
* import tkMessageBox # uvoz paketa za okna z obvestili
* from ScrolledText import * # uvoz pakeza za tekstovno polje

## Methods

* def fizzBuzzMagic(number,tex): # funkcija fizzBuzz
* def main():

## Code

Python tkinter example

    #!/usr/bin/env python
    # -*- coding: utf-8 -*-
    import random
    import Tkinter # uvoz GUI paketa
    import tkMessageBox # uvoz paketa za okna z obvestili
    from ScrolledText import * # uvoz pakeza za tekstovno polje
    
    def fizzBuzzMagic(number,tex): # funkcija fizzBuzz
        while True: # ponavljaj se dokler vnos ni pravilen
            try: # poglej vnos
                number = int(number.get()) # ce je vse ok...
                break # prekini zanko
            except ValueError: # sicer...
               return tkMessageBox.showinfo("Incorrect input type", "Please insert a number!") # javi error
    
        if number > 100 or number < 0 or type(number) != int :  # v kolikor stevilo ni ustrezno se zanka ponovi
            return tkMessageBox.showinfo("Wrong number input","The input number was either too high or too low.\n Make sure the number is between 1 and 100.")
        else:
            tkMessageBox.showinfo("Success", "FIZZ BUZZ TIME!")
    
            for i in range(number):  # stevilo doloci koliko casa naj se izvaja for zanka
    
                output = i + 1  # vsako vrednost v for zanki shranimo v novo spremenljivko
    
                if output % 3 == 0 and output % 5 == 0:  # preverimo ali je trenutna spremenljivka deljiva s 3 in 5. V kolikor je...
                    tex.insert(Tkinter.END,"FizzBuzz\n") # izpisi ta niz
                elif output % 3 == 0:  # V kolikor je stevilo deljivo samo s 3, izpisi...
                    tex.insert(Tkinter.END, "Fizz\n")  # ta niz
                elif output % 5 == 0:  # V kolikor je stevilo deljivo samo s 5, izpisi...
                    tex.insert(Tkinter.END, "Buzz\n")  # ta niz
                else:
                    tex.insert(Tkinter.END, str(output)+"\n")  # Sicer enostavno izpisi vrednost spremenljivke
    
    def main():
        window = Tkinter.Tk() # ustvarimo okno
        window.title("FizzBuzz") # ga poimenujemo
        window.geometry('{}x{}'.format(400, 300)) # dolocimo velikost okna
    
        instructions = Tkinter.Label(window, text="\nPlease insert a number between 1 and 100 in the input field below:") # vstavimo besedilo (navodila)
        instructions.pack(pady=5) # jih dodamo v GUI, razmik med elementi na y osi(vertikalno) naj bo 5
    
    
        number = Tkinter.Entry(window) # polje za vnos stevila
        number.pack(pady=5) # dodamo v GUI
    
        submit = Tkinter.Button(window, text="Submit", command=lambda: fizzBuzzMagic(number,tex)) # gumb, ob kliku naj se klice funkcija
        submit.pack(pady=8) # dodamo v GUI
    
        tex = ScrolledText(window, width=400, height=50) # textovno polje
        tex.pack(pady=8) # dodajmo v GUI
    
    
        window.mainloop() # ukaz za izvajanje GUI
    
    if __name__ == "__main__":
        main() # pozeni metodo main

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

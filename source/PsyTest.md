---
title: PsyTest
date: 2020-05-07
---
Example Python program PsyTest.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import tkinter
* #from tkinter import *
* from tkinter import messagebox,Label,Button,Tk
* import random

## Classes

* class PsyTest:

## Methods

* def GenerateNumber(self):
* def VerifyGuess(self):
* def __init__(self):

## Code

Python tkinter example

    #!/bin/python
    
    '''
    Simple Psychic Test
    
    By: T31337
    '''
    import tkinter
    #from tkinter import *
    from tkinter import messagebox,Label,Button,Tk
    import random
    
    class PsyTest:
        
        MinNumber = 0
        MaxNumber = 100
        NumCorrect = 0
        GuessCorrect = None
        NumGuesses = 0
        number = None
        
        def GenerateNumber(self):
            self.number = random.randint(self.MinNumber,self.MaxNumber)
            self.numberLbl.setvar(name='number',value=self.number)
            self.NumGuesses += 1
            self.VerifyGuess()
            
            
        def VerifyGuess(self):
            print("Will Verfiy Guess Now...")
            WasRight = messagebox.askquestion('PsyTest','Generated Number: '+str(self.number)+'\n Did You Guess Correctly?\n\nPlese Answer Honestly,\n Cheating Won\'t Help Your Psychic Ability, Only Falsify Your Score')
            if WasRight == "yes":
                self.NumCorrect += 1
            messagebox.showinfo(title="PsyTest",message="Score: "+str(self.NumCorrect)+" / "+str(self.NumGuesses)+"\n\nPlease Feel Free To Try Again \n(We Will Keep Track Of Your Score For You)")
    
        def __init__(self):
            print("PsyTest Initating...")
            self.win = Tk()
            self.win.bind("<Return>",self.GenerateNumber)
            self.win.title('PsyTest!')
            
            self.numberLbl = Label(self.win,text="Guess The Number Between 0 & 100, \n Click The Button After Your Guess Is Complete",textvariable='number')
            
            self.btnGuess = Button(self.win,command=self.Generate,text="Generate Number")
            self.btnGuess.bind("<Return>",self.GenerateNumber)
            
            self.numberLbl.grid(row=0,column=0)
            self.btnGuess.grid(row=1,column=0)
            
            self.win.mainloop()
            
        
    if __name__ == "__main__":
        PsyTest()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

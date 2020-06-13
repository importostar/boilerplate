---
title: cjmsMimic
date: 2020-05-07
---
Example Python program cjmsMimic.py

## Modules

* import tkinter
* import random

## Classes

* class ConjuguemosMimic(tkinter.Frame):

## Methods

* def __init__(self, wordLst, master=None):
* def checkAnswer(self):

## Code

Python tkinter example

    import tkinter
    import random
    
    
    class ConjuguemosMimic(tkinter.Frame):
        def __init__(self, wordLst, master=None):
            tkinter.Frame.__init__(self, master)
            self.attempts = 0
            self.order = 0
            self.wordLst = wordLst
            self.lstLen = len(self.wordLst)
            self.wordLstIndex = random.randint(0, len(self.wordLst) - 1)
            self.response = ""
            self.pack()
            # Language settings to be implemented, not ready yet
            # self.LangSet1 = tkinter.Radiobutton(self, text="Spanish-English", variable=self.order, value=0).grid(row=0,
            #                                                                                                      column=0,
            #                                                                                                      columnspan=3)
            # self.LangSet2 = tkinter.Radiobutton(self, text="English-Spanish", variable=self.order, value=1).grid(row=0,
            #                                                                                                      column=3,
            #                                                                                                      columnspan=3)
            self.TranPrompt = tkinter.Label(self, text="Translation:").grid(row=2, column=0, columnspan=2)
            self.Prompt = tkinter.Label(self, text=self.wordLst[self.wordLstIndex][self.order])
            self.Prompt.grid(row=1, column=0, columnspan=6)
            self.TranInput = tkinter.Entry(self)
            self.TranInput.grid(row=2, column=2, columnspan=3)
            self.SubmitButton = tkinter.Button(self, text="Check", command=self.checkAnswer).grid(row=2, column=5)
            self.Feedback = tkinter.Label(self, text="Answer the question.")
            self.Feedback.grid(row=3, column=0, columnspan=6)
    
        def checkAnswer(self):
            self.attempts += 1
            valid = self.wordLst[self.wordLstIndex][self.order - 1] == self.TranInput.get()
            if valid:
                self.wordLst.remove(self.wordLst[self.wordLstIndex])
                self.Feedback.config(text="Correct!")
                self.TranInput.delete(0, len(self.TranInput.get()))
                if len(self.wordLst) > 0:
                    self.wordLstIndex = random.randint(0, len(self.wordLst) - 1)
                    self.Prompt.config(text=self.wordLst[self.wordLstIndex][self.order])
                else:
                    self.Prompt.config(
                        text="Complete! You got " + str(self.lstLen) + "/" + str(self.attempts) + " correct!")
            elif not valid:
                self.Feedback.config(text="The correct answer is " + self.wordLst[self.wordLstIndex][self.order - 1])
    
    
    # Enter a 2d List of vocab to the variable "vocabList"
    vocabList = [['afectar', 'to affect'], ['respetar', 'to respect'],
                 ['aceptar', 'to accept'], ['valorar', 'to value'], ['balancear', 'to balance']]
    root = tkinter.Tk()
    conj = ConjuguemosMimic(vocabList, master=root)
    conj.mainloop()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

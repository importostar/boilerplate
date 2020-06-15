---
title: guessGUIPartial
date: 2020-05-07
---
Example Python program guessGUIPartial.py

## Modules

* import Tkinter
* import tkMessageBox
* import random
* from functools import partial

## Methods

* def check_guess(secret, guess):
* def main():

## Code

Python tkinter example

    import Tkinter
    import tkMessageBox
    import random
    from functools import partial
    
    
    def check_guess(secret, guess):
    
        if int(guess.get()) == secret:
            result_text = "CORRECT!"
        elif int(guess.get()) > secret:
            result_text = "WRONG! Your guess is too high."
        else:
            result_text = "WRONG! Your guess is too low."
    
        tkMessageBox.showinfo("Result", result_text)
    
    
    def main():
    
        window = Tkinter.Tk()
    
        greeting = Tkinter.Label(window, text="Guess the secret number!")
        greeting.pack()
    
        secret = random.randint(1, 100)
    
        guess = Tkinter.Entry(window)
        guess.pack()
    
        check_guess_with_args = partial(check_guess, secret, guess)
        checkButton = Tkinter.Button ( window, text="Check", command=check_guess_with_args )
        checkButton.pack()
    
        resetButton = Tkinter.Button(window, text="Reset", command=main)
        resetButton.pack()
    
        window.mainloop()
    
    
    if __name__ == "__main__":
        main()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

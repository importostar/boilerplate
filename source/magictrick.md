---
title: magictrick
date: 2020-05-07
---
Example Python program magictrick.py

## Modules

* from tkinter import *
* from tkinter import scrolledtext
* from tkinter import messagebox
* from tkinter.ttk import Progressbar
* from tkinter import filedialog
* from tkinter import Menu

## Methods

* def clicked():

## Code

Python tkinter example

    from tkinter import *
    from tkinter import scrolledtext
    from tkinter import messagebox
    from tkinter.ttk import Progressbar
    from tkinter import filedialog
    from tkinter import Menu
    
    window = Tk()
    window.title("Magic Trick")
    
    window.geometry('620x330')
    lbl = Label(window, text = "Steps to follow:", font = ("System",20))
    lbl.grid(column = 0, row = 4, columnspan = 22)
    
    step1 = Label(window, text = "1. Think of any 4 digit number that has at least two unique digits (e.g. 2222 is not accepted!)", font = ("System",14))
    step1.grid(column = 0, row = 8, columnspan = 22)
    
    step2 = Label(window, text = "2. Reverse the 4 digit number. (e.g. 1234 -> 4321)", font = ("System",14))
    step2.grid(column = 0, row = 10, columnspan = 22)
    
    step3 = Label(window, text = "3. Subtract the bigger number from the smaller number (e.g. 4321 - 1234 = 3087)", font = ("System",14))
    step3.grid(column = 0, row = 12, columnspan = 22)
    
    step4 = Label(window, text = "4. Cross out ONE of the nonzero digits. (e.g. 3087 -> cross out 3, 8, or 7)", font = ("System",14))
    step4.grid(column = 0, row = 14, columnspan = 22)
    
    step5 = Label(window, text = "5. Enter the remaining 3 digits (in any order) and I will guess the digit you crossed out!", font = ("System",14))
    step5.grid(column = 0, row = 16, columnspan = 22)
    
    firstdigit = Entry(window, width = 1, font = ("System", 30))
    firstdigit.grid(column = 10, row = 20)
    
    seconddigit = Entry(window, width = 1, font = ("System", 30))
    seconddigit.grid(column = 11, row = 20)
    
    thirddigit = Entry(window, width = 1, font = ("System", 30))
    thirddigit.grid(column = 12, row = 20)
    
    msglbl = Label(window, text = "", font = ("System", 20))
    msglbl.grid(column = 0, row = 40, columnspan = 22)
    
    result = Label(window, text = "", font = ("System", 40))
    result.grid(column = 0, row = 44, columnspan = 22)
    
    def clicked():
        msglbl.configure(text = "The number that you crossed out is")
        sum = int(firstdigit.get()) + int(seconddigit.get()) + int(thirddigit.get())
        div9 = sum // 9
        r = (div9 + 1) * 9
        final = r - sum
        result.configure(text = str(final))
    
    guess = Button(window, text = "Guess!", command = clicked, font = ("System", 20), width = 12)
    guess.grid(column = 1, row = 36, columnspan = 24)
    
    window.mainloop()
    
    # 0. 1. 2. 3. 4. 5. 6. 7. 8. 9. 10 11 12 13. 14. 15. 16. 17. 18. 19. 20. 21. 22.
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

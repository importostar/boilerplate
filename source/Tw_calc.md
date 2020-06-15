---
title: Tw_calc
date: 2020-05-07
---
Example Python program Tw_calc.py

## Modules

* import sys
* from tkinter import *
* from tkinter import Frame
* from typing import List

## Code

Python tkinter example

    # Easy and simple way to use tkinter button widget
    # Import tkinter (*)all modules
    # No functions, only graphic
    
    import sys
    from tkinter import *
    from tkinter import Frame
    from typing import List
    
    app = Tk()
    
    
    floor_4 = Frame(app
                    )
    floor_4.pack()
    app.title("TwCalc"
              )
    no = IntVar()
    # 
    up_floor = Frame(app, bg="white", border=2, )
    up_floor.pack(side=TOP)
    
    #//////// an entry to display digits(input/output) in the top side of the window //////////
    
    Digitprint = Entry(up_floor, textvariable=no, width=18 ,font=30,
                       bd=10 , fg="red" ,bg="yellow"
                       )
    Digitprint.pack(side=TOP)
    # ---------------------------------------------------------------------------------
    # Tkinter button widget (we create button that displays 1,
    # We speciy its position with .pack(side="left,top,right or bottom"),size(pady,padx),
    # Color of the digit (bg="color"),color of the button(fg="color"),
    # Font(font=('arial,broadway,britannic...)more about fonts:open notepad>Format>font
    # All button have the same specification(arguments) in this code 
    #-----------------------------------------------------------------------------------
    button1 = Button(up_floor, padx=20, pady=5, text="1", fg="blue", bg="white",
                     bd=5, font=('Old English Text MT', 10,)
                     )
    button1.pack(side=LEFT)
    button2 = Button(up_floor, padx=20, pady=5, text="2", fg="blue", bg="white",
                     bd=5, font=('Old English Text MT', 10,)
                     )
    button2.pack(side=LEFT)
    button3 = Button(up_floor, padx=20, pady=5, text="3", fg="blue", bg="white",
                     bd=5, font=('Old English Text MT', 10,)
                     )
    button3.pack(side=LEFT)
    
    floor_3 = Frame(app)
    floor_3.pack(side=TOP)
    
    
    button4 = Button(floor_3, padx=20, pady=5, text="4", fg="blue", bg="white",
                     bd=5, font=('Old English Text MT', 10,)
                     )
    button4.pack(side=LEFT)
    button5 = Button(floor_3, padx=20, pady=5, text="5", fg="blue", bg="white",
                     bd=5, font=('Old English Text MT', 10,)
                     )
    button5.pack(side=LEFT)
    button6 = Button(floor_3, padx=20, pady=5, text="6", fg="blue", bg="white",
                     bd=5, font=('Old English Text MT', 10,)
                     )
    button6.pack(side=LEFT)
    
    floor_4 = Frame(app)
    floor_4.pack(side=TOP)
    
    button7 = Button(floor_4, padx=20, pady=5, text="7", fg="blue", bg="white",
                     bd=5, font=('Old English Text MT', 10,)
                     )
    button7.pack(side=LEFT)
    button8 = Button(floor_4, padx=20, pady=5, text="8", fg="blue", bg="white",
                     bd=5, font=('Old English Text MT', 10,)
                     )
    button8.pack(side=LEFT)
    button9 = Button(floor_4, padx=20, pady=5, text="9", fg="blue", bg="white",
                     bd=5, font=('Old English Text MT', 10,)
                     )
    button9.pack(side=LEFT)
    
    floor_5 = Frame(app)
    floor_5.pack(side=TOP)
    
    button7 = Button(floor_5, padx=15, pady=5, text="-", fg="blue", bg="white",
                     bd=5,font=('Old English Text MT', 10,)
                     )
    button7.pack(side=LEFT)
    button8 = Button(floor_5, padx=30, pady=5, text="0", fg="blue", bg="white",
                     bd=5,font=('Old English Text MT', 10,)
                     )
    button8.pack(side=LEFT)
    button9 = Button(floor_5, padx=15, pady=5, text="+", fg="blue", bg="white",
                     bd=5,font=('Old English Text MT', 10,)
                     )
    button9.pack(side=LEFT)
    
    floor_7 = Frame(app)
    floor_7.pack(side=TOP)
    
    button13 = Button(floor_7, padx=20, pady=5, text="+", fg="blue", bg="white",
                      bd=5,font=('Old English Text MT', 10,)
                      )
    
    button13.pack(side=LEFT)
    button14 = Button(floor_7, padx=20, pady=5, text=".", fg="blue", bg="white",
                      bd=5,font=('Old English Text MT', 10,)
                      )
    
    button14.pack(side=LEFT)
    button15 = Button(floor_7, padx=20, pady=5, text="/", fg="blue", bg="white",
                      bd=5,font=('Old English Text MT', 10,)
                      )
    button15.pack(side=LEFT)
    
    floor_8 = Frame(app)
    floor_8.pack(side=TOP)
    
    # "Clear Button" has a width of 78(padx)
    
    buttonc = Button(floor_8, padx=78, pady=5, text="C", fg="red", bg="white",
                     bd=5, font=('Old English Text MT', 10,)
                     )
    buttonc.pack(side=TOP)
    # ------------------------------------------------------------------------------
    app.mainloop()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

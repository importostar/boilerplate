---
title: passgengui
date: 2020-05-07
---
Example Python program passgengui.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import tkinter
* from tkinter import *
* import string
* import random

## Methods

* def pw_gen_low(size = 8, charslow=string.digits):
* def low():
* def pw_gen_medium(size = 8, charsmedium=string.digits + string.ascii_letters):
* def medium():
* def pw_gen_high(size = 8, charshigh=string.digits + string.ascii_letters + string.punctuation):
* def high():
* def strengthlevel():
* def getstrength():

## Code

Python tkinter example

    import tkinter
    from tkinter import *
    import string
    import random
    
    form1 = Tk()
    form1.title("Password Manager")
    #form1.minsize(150,75)
    form1.geometry('275x130')
    
    #StringVars... Needed for the labels and entries.
    #####################################
    # sv1 # Label: How many characters? #
    # sv2 # Input: Characters Entry     #
    # sv3 # Label: Generated Password:  #
    # sv4 # Input: Gen'd Password       #
    # iv1 # Button: Strength Selection  #
    #####################################
    sv1 = StringVar()
    sv2 = StringVar()
    sv3 = StringVar()
    sv4 = StringVar()
    iv1 = IntVar()
    def pw_gen_low(size = 8, charslow=string.digits):
        return ''.join(random.choice(charslow) for _ in range(size))
    def low():
        sv4.set(pw_gen_low(int(sv2.get())))
    
    def pw_gen_medium(size = 8, charsmedium=string.digits + string.ascii_letters):
        return ''.join(random.choice(charsmedium) for _ in range(size))
    def medium():
        sv4.set(pw_gen_medium(int(sv2.get())))
    
    def pw_gen_high(size = 8, charshigh=string.digits + string.ascii_letters + string.punctuation):
        return ''.join(random.choice(charshigh) for _ in range(size))
    def high():
        sv4.set(pw_gen_high(int(sv2.get())))
    
    def strengthlevel():
        print("You have selected " + str(iv1.get()))
    
    def getstrength():
        if iv1.get() == 1:
            low()
        elif iv1.get() == 2:
            medium()
        elif iv1.get() == 3:
            high()
    
    label1 = Label(textvariable=sv1)         #How Many Characters?
    entry1 = Entry(form1,textvariable=sv2)   #Characters Entry
    label2 = Label(textvariable=sv3)         #Generated Password:
    entry2 = Entry(form1,textvariable=sv4)   #Gen'd Password
    button1 = tkinter.Button(form1, text = "Generate", command = getstrength)
    
    sv1.set('Character Count:')
    sv2.set('')
    sv3.set('Password:')
    sv4.set('')
    iv1.set('1')
    
    label1.grid(row=0, column=0)
    entry1.grid(row=0, column=1)
    label2.grid(row=1, column=0)
    entry2.grid(row=1, column=1)
    Radiobutton(form1, text="LOW", variable=iv1, value=1, command=strengthlevel).grid(row=2, column=0, columnspan=2)
    Radiobutton(form1, text="MEDIUM", variable=iv1, value=2, command=strengthlevel).grid(row=3, column=0, columnspan=2)
    Radiobutton(form1, text="HIGH", variable=iv1, value=3, command=strengthlevel).grid(row=4, column=0, columnspan=2)
    button1.grid(row=5, column=0, columnspan=2)
    
    form1.mainloop()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

---
title: tkiner
date: 2020-05-07
---
Example Python program tkiner.py

## Modules

* from tkinter import *
* from tkinter import ttk, Canvas, Frame, BOTH, font

## Methods

* def focusInE1(event):
* def focusOutE1(event):
* def focusInE2(event):
* def focusOutE2(event):

## Code

Python tkinter example

    from tkinter import *
    from tkinter import ttk, Canvas, Frame, BOTH, font
    
    root = Tk() # Skapar fönstret
    
    root.title("SoundCloud") # Fönstertitel 
    
    #root.geometry("400x200") # Fönsterstorlek, BREDDxHÖJD
    root.withdraw()
    root.update_idletasks()  # Update "requested size" from geometry manager
    
    x = (root.winfo_screenwidth() - root.winfo_reqwidth()) / 2
    y = (root.winfo_screenheight() - root.winfo_reqheight()) / 2
    root.geometry("+%d+%d" % (x, y))
    
    # This seems to draw the window frame immediately, so only call deiconify()
    # after setting correct window position
    root.deiconify()
    
    root.configure(background = 'white') # Bakgrundsfärg till fönstret
    
    rootFont = font.Font(family='Arial', size=10, weight='bold')
    
    w_width = 400
    w_height = 200
    w = Canvas(root, width=w_width, height=w_height, # Skapar 'w' canvas't
               borderwidth=2,
               highlightthickness=0,
               background='white')
    
    w.pack() # Vad gör denna? :(
    
    y = int(50)
    w.create_line(20, y, w_width-20, y, fill="#ddd", width=2)
    w.create_line(20, 100, w_width-20, 100, fill="#ddd", width=2)
    
    signin = Button(w, text="Log In", fg="white", bg="#f70", bd="-2", height="3", width="20", command=w.quit, font=rootFont)
    signin.pack(side=LEFT)
    signin.place(relx=.75, rely=.75, anchor="c")
    #
    CheckVar2 = IntVar()
    C2 = Checkbutton(root, text = "Remember me", variable = CheckVar2, onvalue = 1, offvalue = 0, height=2, width = 20, bg="white")
    C2.pack(side=LEFT)
    C2.place(relx=.2, rely=.75, anchor="c")
    # Username input
    username = StringVar()
    username.set("Username")
    E1 = Entry(root, bd = 0, width=59, textvariable=username)
    E1.pack(side=LEFT)
    E1.place(relx=.495, rely=.18, anchor="c")
    # Password input
    password = StringVar()
    password.set('Password')
    E2 = Entry(root, bd = 0, width=59, textvariable=password)
    E2.pack(side=LEFT)
    E2.place(relx=.495, rely=.43, anchor="c")
    
    w.create_line(375, 200, w_width-20, 200, fill="#ddd", width=2)
    
    
    def focusInE1(event):
        w.create_line(20, y, w_width-20, y, fill="#f70", width=2)
        #username.set("")
    
    def focusOutE1(event):
        w.create_line(20, y, w_width-20, y, fill="#ddd", width=2)
        #username.set("Username")
    
    E1.bind("<FocusIn>", focusInE1)
    E1.bind("<FocusOut>", focusOutE1)
    #
    def focusInE2(event):
        w.create_line(20, 100, w_width-20, 100, fill="#f70", width=2)
        #password.set('')
    
    def focusOutE2(event):
        w.create_line(20, 100, w_width-20, 100, fill="#ddd", width=2)
        #password.set("Password")
    
    E2.bind("<FocusIn>", focusInE2)
    E2.bind("<FocusOut>", focusOutE2)
    
    root.mainloop() # Loopar funktionen, för Windows användare endast

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

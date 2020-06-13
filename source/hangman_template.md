---
title: hangman_template
date: 2020-05-07
---
Example Python program hangman_template.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import tkinter
* from tkinter import font

## Classes

* class MyGUI:

## Methods

* def __init__(self):
* def menu_new(self):
* def btn_guess_a_letter_click(self):

## Code

Python tkinter example

    #I McTavish
    #Nov 3, 2016
    #Create a template for hangman game.
    import tkinter
    from tkinter import font
    
    class MyGUI:
        """The class that handles the window"""
        def __init__(self):
            #main window
            self.main_window = tkinter.Tk()
            self.main_window.title("Hangman")
            self.main_window.iconbitmap('favicon.ico')#Requires that file in the folder
            # create a custom font
            self.customFont = font.Font(family="Helvetica", size=36)
            #menus
            self.menubar = tkinter.Menu(self.main_window)
            self.filemenu = tkinter.Menu(self.main_window,tearoff=0)
            self.filemenu.add_command(label="New", command=self.menu_new)
            self.filemenu.add_command(label="Exit",command=self.main_window.quit)
    
            self.menubar.add_cascade(label="File",menu=self.filemenu)
            self.main_window.config(menu = self.menubar)
    
            #frames
            self.topframe = tkinter.Frame(self.main_window)
            self.bottomframe = tkinter.Frame(self.main_window)
            self.topframe.pack()
            self.bottomframe.pack()
    
            #topframeitems - label and canvas
            self.txt_word = tkinter.StringVar()
            self.txt_word.set("_ _ _ _ ")
            print(self.txt_word.get())
            self.lbl_word = tkinter.Label(self.topframe,
                                          textvariable=self.txt_word,
                                          font=self.customFont)
    
            self.canvas = tkinter.Canvas(self.topframe,width=300, height=400)
            self.imagefile=tkinter.PhotoImage(file = "hangman01.png")
            self.canvas.create_image(150, 200, image=self.imagefile)
            self.lbl_word.pack(side="left")
            self.canvas.pack(side='left')
    
            #bottomframe items - pick letters and buttons
            self.alphabet = []
    
            for letters in range(65,(65+26)):
                self.alphabet.append(chr(letters))
            print(self.alphabet)
            self.selected_letter=tkinter.StringVar()
            self.selected_letter.set(self.alphabet[0])
            self.letters_to_pick_from = tkinter.OptionMenu(self.bottomframe,
                                                           self.selected_letter,
                                                           *self.alphabet)
            self.letters_to_pick_from.config(font = self.customFont)
            self.letters_to_pick_from.pack(side='left', padx=10,pady=10)
    
            self.btn_pick_letter = tkinter.Button(self.bottomframe,
                                                  text='guess a letter',
                                                  command = self.btn_guess_a_letter_click,
                                                  font = self.customFont)
            self.btn_pick_letter.pack()
    
            #main loop
            tkinter.mainloop()
    
        def menu_new(self):
            """Runs when new button pressed.  Clears board
            picks a new word
            sets up board"""
            self.imagefile = tkinter.PhotoImage(file = "hangman02.gif")
            self.canvas.create_image(150,200,image=self.imagefile)
            print("in new method")
    
        def btn_guess_a_letter_click(self):
            print(self.selected_letter.get())
    gui = MyGUI()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

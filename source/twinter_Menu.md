---
title: twinter_Menu
date: 2020-05-07
---
Example Python program twinter_Menu.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* from tkinter import *
* from tkinter import messagebox

## Methods

* def quit_app():
* def show_about(event=None):
* def change_font(event=None):

## Code

Python tkinter example

    from tkinter import *
    from tkinter import messagebox
    
    
    # ---------- MENU BARS ----------
    
    # Quits the TkInter app when called
    def quit_app():
        root.quit()
    
    
    # Opens a message box when called
    def show_about(event=None):
        messagebox.showwarning(
            "About",
            "This Awesome Program was Made in 2016"
        )
    
    
    root = Tk()
    
    # Create the menu object
    the_menu = Menu(root)
    
    # ----- FILE MENU -----
    
    # Create a pull down menu that can't be removed
    file_menu = Menu(the_menu, tearoff=0)
    
    # Add items to the menu that show when clicked
    # compound allows you to add an image
    file_menu.add_command(label="Open")
    file_menu.add_command(label="Save")
    
    # Add a horizontal bar to group similar commands
    file_menu.add_separator()
    
    # Call for the function to execute when clicked
    file_menu.add_command(label="Quit", command=quit_app)
    
    # Add the pull down menu to the menu bar
    the_menu.add_cascade(label="File", menu=file_menu)
    
    # ----- FONT MENU FOR VIEW MENU -----
    
    # Stores font chosen and will update based on menu
    # selection
    text_font = StringVar()
    text_font.set("Times")
    
    
    # Outputs font changes
    def change_font(event=None):
        print("Font Picked :", text_font.get())
    
    
    # Define font drop down that will be attached to view
    font_menu = Menu(the_menu, tearoff=0)
    
    # Define radio button options for fonts
    font_menu.add_radiobutton(label="Times",
                              variable=text_font,
                              command=change_font)
    
    font_menu.add_radiobutton(label="Courier",
                              variable=text_font,
                              command=change_font)
    
    font_menu.add_radiobutton(label="Ariel",
                              variable=text_font,
                              command=change_font)
    
    # ----- VIEW MENU -----
    view_menu = Menu(the_menu, tearoff=0)
    
    # Variable changes when line numbers is checked
    # or unchecked
    line_numbers = IntVar()
    line_numbers.set(1)
    
    # Bind the checking of the line number option
    # to variable line_numbers
    view_menu.add_checkbutton(label="Line Numbers",
                              variable=line_numbers)
    
    view_menu.add_cascade(label="Fonts", menu=font_menu)
    
    # Add the pull down menu to the menu bar
    the_menu.add_cascade(label="View", menu=view_menu)
    
    # ----- HELP MENU -----
    help_menu = Menu(the_menu, tearoff=0)
    
    # accelerator is used to show a shortcut
    # OSX, Windows and Linux use the following options
    # Command-O, Shift+Ctrl+S, Command-Option-Q with the
    # modifiers Control, Ctrl, Option, Opt, Alt, Shift,
    # and Command
    help_menu.add_command(label="About",
                          accelerator="command-H",
                          command=show_about)
    
    the_menu.add_cascade(label="Help", menu=help_menu)
    
    # Bind the shortcut to the function
    root.bind('<Command-A>', show_about)
    root.bind('<Command-a>', show_about)
    
    # Display the menu bar
    root.config(menu=the_menu)
    
    root.mainloop()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

---
title: mani
date: 2020-05-07
---
Example Python program mani.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import tkinter
* from tkinter import *
* from tkinter.filedialog import asksaveasfilename
* from PIL import Image, ImageTk, ImageGrab

## Methods

* def exitWindow():
* def save():

## Code

Python tkinter example

    #!/use/bin/env python3
    
    import tkinter
    from tkinter import *
    from tkinter.filedialog import asksaveasfilename
    from PIL import Image, ImageTk, ImageGrab
    
    window = tkinter.Tk()
    window.geometry("520x800")
    window.title("STARLABS BIOSCIENCE SDN BHD")
    window.resizable(False, False)
    window.config(background="#150051")
    
    MENUBAR = Menu(window)
    window.config(menu=MENUBAR)
    
    image = Image.open("s.jpg")
    photo = ImageTk.PhotoImage(image)
    label = Label(window, image=photo, text="", fg="white").pack()
    venuelabel = Label(window, text="Venue: ", background="#150051", fg="white", font=("bold", 13)).place(x=0, y=660)
    contactLabel = Label(window, text="Contact: ", background="#150051", font=("bold", 13), foreground="White").place(x=0,
                                                                                                                      y=720)
    dateTEXT = Entry(window, width=35, font=("bold", 13)).place(x=170, y=380)
    Venue = Text(window, width=35, background="#150051", fg="white", font=("bold", 13)).place(x=72, y=660, height=60)
    person = Entry(window, width=35, background="#150051", fg="white", font=("bold", 13)).place(x=72, y=720)
    
    
    # function :
    def exitWindow():
        window.destroy()
    
    
    def save():
        print("save")
        dialogue = image.filename = asksaveasfilename(initialdir="/", title="Save As", filetypes=(
            ('JPEG', ('*.jpg', '*.jpeg', '*.jpe')), ('PNG', '*.png'), ('BMP', ('*.bmp', '*.jdib')), ('GIF', '*.gif')))
        if result:
            x = window.winfo_rootx()
            y = window.winfo_rooty()
            height = window.winfo_height() + y
            width = window.winfo_width() + x
            ImageGrab.grab().crop((x, y, width, height)).save(result)
    
    
    # Add Menu Items:
    file_menu = Menu(MENUBAR, tearoff=0)
    file_menu.add_cascade(label="Save", command=save)
    addon = Menu(file_menu, tearoff=0)
    addon.add_command(label="SAVE TO FILE")
    addon.add_command(label="Email To")
    file_menu.add_command(label="Exit", command=exitWindow)
    MENUBAR.add_cascade(label="File", menu=file_menu)
    help_menu = Menu(MENUBAR, tearoff=0)
    MENUBAR.add_cascade(label="Help", menu=help_menu)
    
    window.mainloop()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

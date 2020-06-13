---
title: mulitpage
date: 2020-05-07
---
Example Python program mulitpage.py

## Modules

* import tkinter as tk
* from tkinter import ttk

## Classes

* class satApp(tk.Tk):
* class startPage(tk.Frame):
* class pageOne(tk.Frame):
* class pageTwo(tk.Frame):

## Methods

* def __init__(self, *args, **kwargs):
* def show_frame(self, cont):
* def __init__(self, parent, controller):
* def __init__(self, parent, controller):
* def __init__(self, parent, controller):

## Code

Python tkinter example

    import tkinter as tk
    from tkinter import ttk
    # This is where the pe-defined font are going to go ↓
    LARGE_FONT = ("Times New Roman", 12)  # This is defining a font setting so it can just be called
    BUTTON_FONT = ("Times New Roman", 14)
    
    
    class satApp(tk.Tk):
        def __init__(self, *args, **kwargs):
            tk.Tk.__init__(self, *args, **kwargs)
            tk.Tk.iconbitmap(self, r"C:\Users\Alexander\Desktop\sentdexTkinter\gg.gif")
            container = tk.Frame(self)
            container.pack(side="top", fill="both", expand=True)
            container.grid_rowconfigure(0, weight=1)
            container.grid_columnconfigure(0, weight=1)
    
    
            self.frames = {}
    # This for loop is what raises specified page when adding more pages simply
    # add the class name to the for loop
            for F in (startPage, pageOne, pageTwo):
                frame = F(container, self)
                self.frames[F] = frame
                frame.grid(row=0, column=0, sticky="nsew")
    
            self.show_frame(startPage)
    
        def show_frame(self, cont):
            frame = self.frames[cont]
            frame.tkraise()
    
    # -------------------------------------------------
    
    
    class startPage(tk.Frame):
        def __init__(self, parent, controller):
            tk.Frame.__init__(self, parent)
            label = tk.Label(self, text="Start Page", font=LARGE_FONT)
            label.pack(pady=10, padx=10)
            btnMove = ttk.Button(self, text="Page 1",
                                command=lambda: controller.show_frame(pageOne))
            btnMove.pack()
    # Use this "startPage" as a template for all other tkinter pages
    
    
    class pageOne(tk.Frame):
        def __init__(self, parent, controller):
            tk.Frame.__init__(self, parent)
            label = tk.Label(self, text="Page 1", font=LARGE_FONT)
            label.pack(pady=10, padx=10)
            btnPage2 = ttk.Button(self, text="Page 2",
                                 command=lambda: controller.show_frame(pageTwo))
            btnPage2.pack()
            btnMove = ttk.Button(self, text="Back to home",
                                command=lambda: controller.show_frame(startPage))
            btnMove.pack()
    
    
    class pageTwo(tk.Frame):
        def __init__(self, parent, controller):
            tk.Frame.__init__(self, parent)
            label = tk.Label(self, text="Page 2", font=LARGE_FONT)
            label.pack(pady=10, padx=10)
            btnPage1 = ttk.Button(self, text="Back to page 1",
                                 command=lambda: controller.show_frame(pageOne))
            btnPage1.pack()
    
            btnMove = ttk.Button(self, text="Back to home",
                                command=lambda: controller.show_frame(startPage))
            btnMove.pack()
    
    
    app = satApp()
    app.geometry("400x400")
    app.mainloop()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

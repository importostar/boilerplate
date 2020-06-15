---
title: tkinter stub app
date: 2020-05-07
---
Example Python program tkinter-stub-app.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import tkinter as tk
* from tkinter import *
* from tkinter import messagebox, simpledialog, filedialog, StringVar, ttk
* import os
* import sys, platform, traceback
* import time

## Classes

* class StdoutRedirector(object): # https://stackoverflow.com/q/18517084
* class AppWindow(tk.Frame):

## Methods

* def __init__(self, text_widget):
* def write(self,string):
* def __init__(self, master=None):
* def create_splash(self):
* def center(self):
* def print(self, write):
* def clear(self):
* def reload_app(self):
* def save_console_to_file(self):
* def open_file_dialog(self, types=("all files", "*.*")):
* def save_file_dialog(self, name="File", types=("all files", "*.*")):
* def get_integer_dialog(self, title="Input", prompt="Enter a number"):
* def show_yes_no_dialog(self, title="Input", prompt="Yes or No?"):

## Code

Python tkinter example

    import tkinter as tk
    from tkinter import *
    from tkinter import messagebox, simpledialog, filedialog, StringVar, ttk
    import os
    
    import sys, platform, traceback
    import time
    
    
    
    class StdoutRedirector(object): # https://stackoverflow.com/q/18517084
        def __init__(self, text_widget):
            self.text_space = text_widget
    
        def write(self,string):
            self.text_space.insert('end', string)
            self.text_space.see('end')
    
    
    class AppWindow(tk.Frame):
        def __init__(self, master=None):
            super().__init__(master)
            self.pack()
    
            # Basic Buttons
            self.buttons = {self.reload_app: "Reload Program",
                            self.save_console_to_file: "Save Console to File",
                            self.clear: "Clear Console"}
    
            # Basic Config
            self.config = {"console_WxH": (120, 40),
                           "redirect_stdout": True,
                           "redirect_stderr": True}
    
            # Use with:
            # self.config.get("include_macro_number", False)
    
    
            self.create_splash()
            self.center()
    
            if self.config.get("redirect_stdout", False):
                sys.stdout = StdoutRedirector(self.console)
    
            if self.config.get("redirect_stderr", False):
                sys.stderr = StdoutRedirector(self.console)
    
        def create_splash(self):
            for func in self.buttons.keys():
                tk.Button(command=func, text=self.buttons.get(func)).pack()
            dim = self.config.get("console_WxH", (120, 40))
            self.console = Text(width=dim[0], height=dim[1], borderwidth=2, relief=RIDGE)
            self.console.pack(fill=BOTH, expand=1)
    
        def center(self):
            # https://stackoverflow.com/a/10018670
            self.master.update_idletasks()
            width = self.master.winfo_width()
            height = self.master.winfo_height()
            x = (self.master.winfo_screenwidth() // 2) - (width // 2)
            y = (self.master.winfo_screenheight() // 2) - (height // 2)
            self.master.geometry('{}x{}+{}+{}'.format(width, height, x, y))
            # self.master.minsize(width=width, height=height)
            # self.master.maxsize(width=width, height=height)
    
        def print(self, write):
            self.console.insert(END, str(write) + "\n")
    
        def clear(self):
            self.console.delete(0.0, END)
    
        def reload_app(self):
            python = sys.executable
            os.execl(python, python, *sys.argv)
    
        def save_console_to_file(self):
            dest = self.save_file_dialog(types=(("MD file", "*.md"), ("all files", "*.*")))
            data_to_write = self.console.get(1.0, END)
    
            try:
                file = open(dest, "w")
                file.write(data_to_write)
                file.close()
            except FileNotFoundError:
                print("Invalid File")
    
    
        #############################################
        #############################################
    
        # ############ App Goes Here ############## #
    
        #############################################
        #############################################
    
    
        def open_file_dialog(self, types=("all files", "*.*")):
            # Example Type:
            # types = (("XML files", "*.xml"), ("all files", "*.*"))
    
            return filedialog.askopenfilename(title="Select file", filetypes=types)
    
        def save_file_dialog(self, name="File", types=("all files", "*.*")):
            # Example Type:
            # types = (("XML files", "*.xml"), ("all files", "*.*"))
    
            return filedialog.asksaveasfilename(title="Save file", initialfile=name, filetypes=types)
    
    
        def get_integer_dialog(self, title="Input", prompt="Enter a number"):
            return simpledialog.askinteger(title, prompt)
    
        def show_yes_no_dialog(self, title="Input", prompt="Yes or No?"):
            return messagebox.askyesno(title, prompt)
    
    
    
    
    if __name__ == "__main__":
        app = AppWindow()
        app.mainloop()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

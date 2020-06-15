---
title: TkInterNotepad
date: 2020-05-07
---
Example Python program TkInterNotepad.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import tkinter as tk
* from tkinter.scrolledtext import ScrolledText

## Classes

* class MainWindow(tk.Frame):
* class DialogWindow(tk.Frame):
* class HelpWindow(tk.Frame):

## Methods

* def __init__(self, parent, *args, **kwargs):
* def __build_dialog(self, label, button, *current_file):
* def __build_gui(self):
* def __build_menu(self):
* def help(self):
* def open(self):
* def save(self):
* def exit(self):
* def __init__(self, parent):
* def build(self):
* def set_labels(self, label, button, *current_file):
* def __action(self, data):
* def __init__(self, parent):
* def __build(self):
* def main():

## Code

Python tkinter example

    import tkinter as tk
    from tkinter.scrolledtext import ScrolledText
    
    
    """
        Simplistic example of the GUI creation tools provided by TkInter. Functions as a basic notepad, allowing the user to
        open, edit and save text files.
    """
    
    
    class MainWindow(tk.Frame):
        def __init__(self, parent, *args, **kwargs):
            tk.Frame.__init__(self, parent, *args, **kwargs)
    
            self.root = parent
            self.current_file = None
    
            self.__build_gui()
    
        def __build_dialog(self, label, button, *current_file):
            try:
                dialog_window = DialogWindow(self.root)
                dialog_window.set_labels(label, button, *current_file)
                dialog_window.build()
    
                self.wait_window(dialog_window)
    
                return dialog_window.input
            except KeyboardInterrupt:
                exit()
    
        def __build_gui(self):
            self.root.title("Notepad")
            self.root.option_add('*tearOff', 'FALSE')
    
            frame = tk.Frame(master=self.root)
            frame.pack(fill='both', expand='yes')
    
            # Add text widget to display logging info
            self.st = ScrolledText(frame)
            self.st.configure(font='TkFixedFont')
            self.st.pack(fill=tk.BOTH, expand=True)
    
            self.__build_menu()
    
        def __build_menu(self):
            menu = tk.Menu(self)
    
            file_menu = tk.Menu(menu)
            file_menu.add_command(label="Open file", command=self.open)
            file_menu.add_command(label="Save to file", command=self.save)
            file_menu.add_separator()
            file_menu.add_command(label="Quit", command=self.exit)
    
            menu.add_cascade(label="File", menu=file_menu)
    
            help_menu = tk.Menu(menu)
            help_menu.add_command(label="Help pages", command=self.help)
    
            menu.add_cascade(label="Help", menu=help_menu)
    
            self.root.config(menu=menu)
    
        def help(self):
            try:
                help_window = HelpWindow(self.root)
                self.wait_window(help_window)
            except KeyboardInterrupt:
                exit()
    
        def open(self):
            new_file = self.__build_dialog("File to open", "Open")
    
            if not new_file:
                return
    
            self.current_file = new_file
    
            try:
                with open(self.current_file, "r") as inputFile:
                    self.st.delete(1.0, tk.END)
                    self.st.insert(tk.INSERT, inputFile.read())
            except (FileNotFoundError, OSError) as ex:
                print(ex)
    
        def save(self):
            f = self.__build_dialog("File to save", "Save", self.current_file)
    
            if not f:
                return
    
            try:
                with open(f, "w") as outputFile:
                    outputFile.write(self.st.get(1.0, tk.END))
            except (FileNotFoundError, OSError) as ex:
                print(ex)
    
        def exit(self):
            self.destroy()
            self.root.destroy()
    
    
    class DialogWindow(tk.Frame):
        def __init__(self, parent):
            tk.Frame.__init__(self, parent)
            self.root = tk.Toplevel(parent)
            self.root.resizable(0, 0)
    
            self.label = None
            self.button = None
            self.current_file = None
    
            self.input = None
    
        def build(self):
            l = tk.Label(self.root, width=15, text=self.label)
            l.pack(side=tk.TOP)
    
            e = tk.Entry(self.root)
            if self.current_file:
                e.insert(tk.END, self.current_file)
            e.pack(side=tk.LEFT, padx=20, pady=20)
    
            b = tk.Button(self.root, text=self.button, command=lambda: self.__action(e.get()))
            b.pack(side=tk.RIGHT, padx=20, pady=20)
    
        def set_labels(self, label, button, *current_file):
            self.label = label
            self.button = button
    
            if current_file:
                self.current_file = current_file
    
        def __action(self, data):
            self.input = data
            self.destroy()
            self.root.destroy()
    
    
    class HelpWindow(tk.Frame):
        def __init__(self, parent):
            tk.Frame.__init__(self, parent)
            self.root = tk.Toplevel(parent)
            self.__build()
    
        def __build(self):
            st = ScrolledText(self.root)
            st.pack(padx=10, pady=10, fill=tk.BOTH, expand=True)
    
            help_text = "Help pages\n\n"
            help_text += "About\n"
            help_text += "  Example GUI application in Python using TkInter\n"
            help_text += "  Created by Siegrest\n"
            help_text += "  Version 1.0.0\n"
            help_text += "Usage\n"
            help_text += "  Open file by defining either is absolute path or local path\n"
            help_text += "  Save file by defining either is absolute path or local path\n"
    
            st.insert(tk.INSERT, help_text)
    
    
    def main():
        root = tk.Tk()
        MainWindow(root)
    
        try:
            root.mainloop()
        except KeyboardInterrupt:
            return
    
    
    if __name__ == "__main__":
        main()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

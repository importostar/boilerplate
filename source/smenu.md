---
title: smenu
date: 2020-05-07
---
Example Python program smenu.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import argparse
* import tkinter as tk
* from tkinter import messagebox
* import fileinput
* import subprocess
* import os
* #import pdb

## Methods

* def filter_items(needle):
* def on_keyrelease(event):
* def listbox_update(data):
* def on_select(event):
* def app_lost_focus(event):
* def on_key_press(e):
* def key_escape(e):
* def key_return(e):
* def select_previous(e):
* def select_next(e):
* def do_nothing(event):

## Code

Python tkinter example

    #!/usr/bin/env python3
    
    import argparse
    import tkinter as tk
    from tkinter import messagebox
    import fileinput
    import subprocess
    import os
    #import pdb
    
    _DEBUGGING = False
    
    parser = argparse.ArgumentParser(
        description="Simple tkinter menu app inspired by dmenu, which prints selection to stdout.",
        epilog="Have fun.")
    
    parser.add_argument('-i', '--input', default='-', help="file to read from")
    parser.add_argument('-x', '--execute-output', action='store_true', help="execute the selection.")
    parser.add_argument('-s', '--split-input', action='store_true', help="split input using ';' e.g. key;value")
    
    args = parser.parse_args()
    
    if _DEBUGGING:
        print(args)
    
    items = {}
    
    for line in fileinput.input(files=args.input):
        #pdb.set_trace()
        if line.strip() == "":
            pass
        elif args.split_input:
            try:
                lhs, rhs = (x.strip() for x in line.split(';', 1))
            except ValueError:
                lhs, rhs = line.strip(), ""
            items[lhs] = rhs
        else:
            lhs, rhs = line.strip(), ""
            items[lhs] = lhs
    
    def filter_items(needle):
        return [item for item in items.keys() if needle in item.lower()]
    
    def on_keyrelease(event):
        needle = event.widget.get()
        needle = needle.strip().lower()
    
        if needle == '':
            data = items.keys()
        else:
            data = filter_items(needle)
    
        listbox_update(data)
    
    
    def listbox_update(data):
        listbox.delete(0, 'end')
    
        for item in data:
            listbox.insert('end', item)
    
        listbox.select_set(0)
    
    
    def on_select(event):
        selection = event.widget.get(event.widget.curselection())
    
        if args.split_input:
            selection = items[selection]
    
        if args.execute_output:
            root.withdraw() # hide
            try:
                os.startfile(os.path.normpath(selection))
                #try:
                    #os.startfile(selection)
                    ##subprocess.Popen([selection])
                #except OSError:
                    #os.startfile(selection)
    
                #if selection.endswith('.lnk') or selection.endswith('.url'):
                    #os.startfile(selection)
                #else:
                    #subprocess.Popen([selection])
    
                if _DEBUGGING:
                    print(selection)
            except FileNotFoundError:
                if _DEBUGGING:
                    print(f'can\'t find {selection}')
                messagebox.showerror("Missing file...", f"Failed to find {selection}")
                print(2)
        else:
            print(selection)
    
        root.destroy()
    
    
    # --- main ---
    
    
    def app_lost_focus(event):
        if root.focus_get() == None:
            root.destroy()
    
    
    def on_key_press(e):
        print(e)
    
    
    def key_escape(e):
        if entry.get() == "":
            root.destroy()
        else:
            entry.delete(0, tk.END)
    
    
    def key_return(e):
        if listbox.curselection():
            listbox.event_generate("<<ListboxSelect>>")
        else:
            root.destroy()
    
    def select_previous(e):
        first = listbox.curselection()
    
        if first:
            index = first[0] - 1
        else:
            index = 0
    
        listbox.selection_clear(0, 'end')
        listbox.selection_set(index)
    
    
    def select_next(e):
        first = listbox.curselection()
    
        if first:
            index = first[0] + 1
        else:
            index = 0
    
        listbox.selection_clear(0, 'end')
        listbox.selection_set(index)
    
    def do_nothing(event):
        pass
    
    root = tk.Tk()
    root.title("Py Launcher")
    root.resizable(False, False)
    root.overrideredirect(True)
    root.bind("<FocusOut>", app_lost_focus)
    #root.bind("<Key>", on_key_press)
    root.bind("<Escape>", key_escape)
    root.bind("<Return>", key_return)
    root.bind("<Tab>", key_escape)
    #root.bind("<Up>", key_return)
    
    
    entry = tk.Entry(root)
    entry.config(width=30, font=('', 32))
    entry.pack()
    entry.bind('<KeyRelease>', on_keyrelease)
    entry.bind("<KeyRelease-Up>", select_previous)
    entry.bind("<Down>", select_next)
    entry.bind("<KeyRelease-Down>", do_nothing)
    entry.focus()
    
    listbox = tk.Listbox(root)
    listbox.config(width=30, font=('', 32))
    listbox.pack()
    listbox.bind('<Double-Button-1>', on_select)
    listbox.bind('<<ListboxSelect>>', on_select)
    listbox_update(items.keys())
    
    root.update_idletasks()
    
    WIN_WIDTH = root.winfo_width()
    WIN_HEIGHT = root.winfo_height()
    
    screen_width = root.winfo_screenwidth()
    screen_height = root.winfo_screenheight()
    
    start_x = int((screen_width/2) - (WIN_WIDTH/2))
    start_y = int((screen_height/2) - (WIN_HEIGHT/2))
    
    root.geometry('{}x{}+{}+{}'.format(WIN_WIDTH, WIN_HEIGHT, start_x, start_y))
    
    # print(root.winfo_geometry())
    
    root.mainloop()
    
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

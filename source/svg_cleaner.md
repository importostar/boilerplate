---
title: svg_cleaner
date: 2020-05-07
---
Example Python program svg_cleaner.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import sys
* import tkinter as tk
* from tkinter import filedialog
* from tkinter import messagebox
* import re

## Methods

* def clean_svg_file(content):
* def file_save(text):
* def file_open():

## Code

Python tkinter example

    import sys
    import tkinter as tk
    from tkinter import filedialog
    from tkinter import messagebox
    import re
    
    
    def clean_svg_file(content):
        replacement = content
        for nsName in tags:
            print(nsName)
            reg_xmlns = 'xmlns:' + nsName + '=".*?"\\s*'
            reg_tag = '<' + nsName + ':([^>]|[\\s])*?((\\/>)|(>[\\s\\S]*?<\\/' + nsName + ':.*?>))\\s*'
            reg_attr = nsName + ':.*?=".*?"\\s*'
            replacement = re.sub(reg_xmlns, '', replacement)
            replacement = re.sub(reg_tag, '', replacement)
            replacement = re.sub(reg_attr, '', replacement)
    
        return replacement
    
    
    def file_save(text):
        f = filedialog.asksaveasfile(mode='w', defaultextension=".svg")
        if f is None:  # asksaveasfile return `None` if dialog closed with "cancel".
            return
    
        f.write(text)
        f.close()
        messagebox.showinfo("Information", "File has been cleaned.")
    
    
    def file_open():
        file_path = filedialog.askopenfilename(defaultextension=".svg")
        with open(file_path) as f:
            read_data = f.read()
            f.close()
            return read_data
    
    
    try:
        root = tk.Tk()
        root.withdraw()
        tags = ['inkscape', 'sodipodi', 'rdf', 'cc', 'dc', 'metadata']
    
        file_data = file_open()
    
        question = messagebox.askokcancel("Clean file", "Do you want to clean the file from "
                                                        "'inkscape', 'sodipodi', 'rdf', 'cc', 'dc', 'metadata")
    
        if question:
            cleaned = clean_svg_file(file_data)
            file_save(cleaned)
    
    
    
        sys.exit(0)
    except:
        print(sys.exc_info()[0])
        messagebox.showerror("Error", "Could not clean file\n" + str(sys.exc_info()[0]))
        raise
        sys.exit(1)
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

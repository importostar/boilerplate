---
title: u4pakGUI
date: 2020-05-07
---
Example Python program u4pakGUI.py

## Modules

* import os
* import sys
* import tkinter as tk
* from tkinter import filedialog
* from tkinter import simpledialog
* from tkinter import ttk

## Classes

* class GUI(tk.Tk):

## Methods

* def __init__(self, *args, **kwargs):
* def select_folder(self):
* def pack(self):

## Code

Python tkinter example

    #NOTE: This script is intended to be frozen. If you want to use it as is, replace pyinstaller's specific paths (sys._MEIPASS)
    
    
    # -*- coding: utf-8 -*-
    
    import os
    import sys
    import tkinter as tk
    from tkinter import filedialog
    from tkinter import simpledialog
    from tkinter import ttk
    
    
    class GUI(tk.Tk):
        def __init__(self, *args, **kwargs):
            tk.Tk.__init__(self, *args, **kwargs)
            self.title("u4pak GUI")
            self.geometry("425x175")
    
            self.folder=tk.StringVar()
            self.lbl_folder = ttk.Label(text = "Nimbus folder path:")
            self.lbl_folder.grid(row="0", column="0", padx=(20,0), pady=(10,0))
            self.txtbx_folder=ttk.Entry(self, width=52, textvariable=self.folder)
            self.txtbx_folder.grid(row="1", column="0", padx=(20,0))
    
            self.filename=tk.StringVar()
            self.lbl_filename = ttk.Label(text = "Output file name (without .pak):")
            self.lbl_filename.grid(row="2", column="0", padx=(20,0), pady=(20,0))
            self.txtbx_filename=ttk.Entry(self, width=52, textvariable=self.filename)
            self.txtbx_filename.grid(row="3", column="0", padx=(20,0))
    
            self.btn_selectfolder = ttk.Button(self, text=u'Browse...', command=self.select_folder)
            self.btn_selectfolder.grid(row="1", column="1", padx=(10,0))
    
            self.btn_pack = ttk.Button(self, text=u'PACK', command=self.pack)
            self.btn_pack.grid(row="4", column="0", pady=(35,0), columnspan=2, sticky="news")
    
    
        def select_folder(self):
            folder_path = filedialog.askdirectory(initialdir=".", title="Select your Nimbus folder")
            self.txtbx_folder.delete(0, "end")
            self.txtbx_folder.insert(tk.END, folder_path)
    
    
        def pack(self):
            folder_path = str(self.folder.get())
            folder_path = f'"{folder_path}"'
    
            filename = str(self.filename.get())
            filename = f'"{filename}"'
    
            exec_path = sys._MEIPASS + "/"
            os.system(exec_path + "u4pak.exe pack "+ filename + ".pak " + folder_path) #change u4pak.exe with the name of your script, be it .py or a frozen .exe
    
    
    gui = GUI()
    gui.resizable(False, False)
    gui.mainloop()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

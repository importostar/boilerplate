---
title: dualpane mockup
date: 2020-05-07
---
Example Python program dualpane-mockup.py

## Modules

* import sys
* 	from tkinter import *
* 	from tkinter import ttk
* 	from Tkinter import *
* 	import ttk

## Methods

* def nop():
* def make_pane(parent):

## Code

Python tkinter example

    #!/usr/bin/python3
    
    import sys
    if sys.version_info.major >= 3:
    	from tkinter import *
    	from tkinter import ttk
    else:
    	from Tkinter import *
    	import ttk
    
    def nop():
    	pass
    
    top = Tk()
    top.title("Dual-pane file manager mockup")
    
    buttons = [("Help", nop), ("Menu", nop),
    	("View", nop), ("Edit", nop), ("Copy", nop),
    	("RenMov", nop), ("Mkdir", nop), ("Delete", nop),
    	("PullDn", nop), ("Quit", top.destroy)]
    toolbar = ttk.Frame(top)
    toolbar.pack(side=BOTTOM, fill="x", padx=4, pady=4)
    for lbl, cmd in buttons:
    	button = ttk.Button(toolbar, text=lbl, command=cmd)
    	button.pack(side=LEFT)
    
    cmdline = ttk.Entry(top)
    cmdline.pack(side=BOTTOM, fill="x", padx=4, pady=4)
    
    panes = ttk.PanedWindow(top, orient=HORIZONTAL)
    
    lpane = ttk.Frame(top)
    rpane = ttk.Frame(top)
    panes.add(lpane, weight=1)
    panes.add(rpane, weight=1)
    
    def make_pane(parent):
    	fmpane = ttk.Treeview(parent,
    		columns="name type size date", show="headings", height=25)
    
    	fmpane.column("name", width=220)
    	fmpane.heading("name", text="Name")
    	fmpane.column("type", width=60)
    	fmpane.heading("type", text="Type")
    	fmpane.column("size", width=60)
    	fmpane.heading("size", text="Size")
    	fmpane.column("date", width=60)
    	fmpane.heading("date", text="Date")
    	fmpane.pack(side=LEFT, fill="both", expand=TRUE)
    
    	scroll = ttk.Scrollbar(parent, orient=VERTICAL, command=fmpane.yview)
    	fmpane["yscrollcommand"] = scroll.set
    	scroll.pack(side=RIGHT, fill="y")
    
    	return fmpane
    
    lfiles = make_pane(lpane)
    rfiles = make_pane(rpane)
    
    panes.pack(fill="both", expand=TRUE)
    
    top.option_add('*tearOff', FALSE)
    
    menubar = Menu(top)
    top["menu"] = menubar
    
    mnu_left = Menu(menubar)
    menubar.add_cascade(menu=mnu_left, label="Left", underline=0)
    mnu_left.add_command(label="Sort order...", underline=0)
    
    mnu_file = Menu(menubar)
    menubar.add_cascade(menu=mnu_file, label="File", underline=0)
    mnu_file.add_command(label="View", underline=0, accelerator="F3")
    mnu_file.add_command(label="Edit", underline=0, accelerator="F4")
    mnu_file.add_separator()
    mnu_file.add_command(
    	label="Quit", underline=0, accelerator="F10", command=top.destroy)
    
    mnu_command = Menu(menubar)
    menubar.add_cascade(menu=mnu_command, label="Command", underline=0)
    mnu_command.add_command(label="User menu", underline=0, accelerator="F2")
    
    mnu_options = Menu(menubar)
    menubar.add_cascade(menu=mnu_options, label="Options", underline=0)
    mnu_options.add_command(label="Configuration", underline=0)
    
    mnu_right = Menu(menubar)
    menubar.add_cascade(menu=mnu_right, label="Right", underline=0)
    mnu_right.add_command(label="Sort order...", underline=0)
    
    top.bind("<F10>", lambda e: top.destroy())
    
    top.mainloop()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

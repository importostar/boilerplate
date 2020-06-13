---
title: shell
date: 2020-05-07
---
Example Python program shell.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import Tkinter as tkinter
* from tkinter import *
* import sys, os

## Methods

* def quickload_1():
* def quickload_2():
* def quickload_3():
* def quickload_4():
* def quickload_5():
* def userinput(inp):
* def cmd_help(arguments):
* def cmd_load(arguments):
* def cmd_clear(arguments):
* def func_returninput(event):

## Code

Python tkinter example

    try:
        import Tkinter as tkinter
    except:
        pass
    
    from tkinter import *
    import sys, os
    print("""
    ------------------------------------
                Debug Build
    ------------------------------------
    All errors will be output to console
    ------------------------------------""")
    
    
    #========================================
    #Window Setup
    root = Tk()
    root.title("OSMT")
    root.configure(background="white")
    root.resizable(width=False, height=False)
    
    #========================================
    
    #========================================
    #Asthetics :3
    file_logo = PhotoImage(file="logo.gif")
    element_logo = Label(root, image=file_logo)
    element_logo.photo = file_logo
    element_logo.grid(row=0, column=0)
    
    element_logo_text = Label(root, text="""
    Open Source Multi Tool
    Version 1
    Developed by William Scargill and Jacob Walker
    ----------------------------------------------
    Debug Build
    ----------------------------------------------""", bg="white")
    element_logo_text.grid(row=0, column=1)
    
    #========================================
    
    #=============================================================
    #Quick Load Button Setup
    def quickload_1():
        element_terminal_display.insert(END, "Quick Load 1")
        element_terminal_display.see(END)
    
    def quickload_2():
        element_terminal_display.insert(END, "Quick Load 2")
        element_terminal_display.see(END)
    
    def quickload_3():
        element_terminal_display.insert(END, "Quick Load 3")
        element_terminal_display.see(END)
    
    def quickload_4():
        element_terminal_display.insert(END, "Quick Load 4")
        element_terminal_display.see(END)
    
    def quickload_5():
        element_terminal_display.insert(END, "Quick Load 5")
        element_terminal_display.see(END)
    
    
    element_menu = Menu(root)
    element_menu.add_command(label="Quick Load 1", command=quickload_1)
    element_menu.add_command(label="Quick Load 2", command=quickload_2)
    element_menu.add_command(label="Quick Load 3", command=quickload_3)
    element_menu.add_command(label="Quick Load 4", command=quickload_4)
    element_menu.add_command(label="Quick Load 5", command=quickload_5)
    
    root.config(menu=element_menu)
    #=============================================================
    
    #========================================
    #User Input Function
    
    cwd = os.getcwd()
    
    def userinput(inp):
        
        
        def cmd_help(arguments):
            element_terminal_display.insert(END, "HELP                  ")
            element_terminal_display.see(END)
            element_terminal_display.insert(END, "======================")
            element_terminal_display.see(END)
            for command in commands.keys():
                argstring = ""
                for arg in commands[command]["args"]:
                    argstring += " <" + arg + ">"
                element_terminal_display.insert(END, command + argstring + " - " + commands[command]["help"])
                element_terminal_display.see(END)
                
        def cmd_load(arguments):
            pass
        def cmd_clear(arguments):
             element_terminal_display.delete(0, 20)
    
        
        commands = {
        "help": {
            "help": "Shows this message",
            "execute": cmd_help,
            "args": []
        },
        "load": {
            "help": "Load a module",
            "execute": cmd_load,
            "args": ["module name"]
        },
        "clear": {
            "help": "Clears the screen",
            "execute": cmd_clear,
            "args": []
        },
        }
        while True:
            try:
               os.chdir(cwd)
               inputcommand = inp
               splitcommand = inputcommand.split(" ") # convert to array at each space
               command = splitcommand[0] # first item of array is our command
               splitcommand.pop(0) # remove the first item to get args list
               arguments = splitcommand # create new args list
    
               if command in commands.keys():
                   for icommand in commands.keys():
                       if icommand == command:
                           if len(arguments) < len(commands[command]["args"]):
                               element_terminal_display.insert(END, "You missed some arguments. Type `help` for a list of commands.")
                               element_terminal_display.see(END)
                           else:
                               if command == "exit":
                                   commands[command]["execute"](1)
                               else:
                                   commands[command]["execute"](arguments)
               elif command == "":
                 pass
               else:
                   element_terminal_display.insert(END, "Invalid command. Type `help` for a list of commands.")
                   element_terminal_display.see(END)
            except:
               element_terminal_display.insert(END, "Unexpected error:", sys.exc_info()[0])
               element_terminal_display.see(END)
        
        
    
            
    #========================================
    
    
    #========================================
    #Terminal Setup
    element_terminal_display = Listbox(root, height=20, width=100)
    element_terminal_display.grid(row=1, column=3)
    for i in range(element_terminal_display.cget('height')-1):
        element_terminal_display.insert(END, '')
    element_terminal_entry = Entry(root, width=100)
    element_terminal_entry.grid(row=2, column=3)
    
    
    
    def func_returninput(event):
        inp = element_terminal_entry.get()
        element_terminal_display.insert(END, element_terminal_entry.get())
        element_terminal_display.see(END)
        element_terminal_entry.delete(0, END)
        userinput(inp)
        
    
    root.bind('<Return>', func_returninput)
    #========================================
    root.mainloop()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

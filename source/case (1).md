---
title: case (1)
date: 2020-05-07
---
Example Python program case (1).py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import sys
* import Tkinter as tk
* import tkinter as tk
* import ttk
* import tkinter.ttk as ttk
* import case_support
* '''Starting point when module is imported by another program.'''

## Classes

* class Toplevel1:

## Methods

* def vp_start_gui():
* def create_Toplevel1(root, *args, **kwargs):
* def destroy_Toplevel1():
* def __init__(self, top=None):
* def clearState(self):

## Code

Python tkinter example

    #! /usr/bin/env python
    #  -*- coding: utf-8 -*-
    #
    # GUI module generated by PAGE version 4.26
    #  in conjunction with Tcl version 8.6
    #    Nov 12, 2019 04:17:41 PM CST  platform: Windows NT
    
    import sys
    
    try:
        import Tkinter as tk
    except ImportError:
        import tkinter as tk
    
    try:
        import ttk
        py3 = False
    except ImportError:
        import tkinter.ttk as ttk
        py3 = True
    
    import case_support
    
    def vp_start_gui():
        '''Starting point when module is the main routine.'''
        global val, w, root
        root = tk.Tk()
        case_support.set_Tk_var()
        top = Toplevel1 (root)
        case_support.init(root, top)
        root.mainloop()
    
    w = None
    def create_Toplevel1(root, *args, **kwargs):
        '''Starting point when module is imported by another program.'''
        global w, w_win, rt
        rt = root
        w = tk.Toplevel (root)
        case_support.set_Tk_var()
        top = Toplevel1 (w)
        case_support.init(w, top, *args, **kwargs)
        return (w, top)
    
    def destroy_Toplevel1():
        global w
        w.destroy()
        w = None
    
    class Toplevel1:
        def __init__(self, top=None):
            '''This class configures and populates the toplevel window.
               top is the toplevel containing window.'''
            _bgcolor = '#d9d9d9'  # X11 color: 'gray85'
            _fgcolor = '#000000'  # X11 color: 'black'
            _compcolor = '#d9d9d9' # X11 color: 'gray85'
            _ana1color = '#d9d9d9' # X11 color: 'gray85'
            _ana2color = '#ececec' # Closest X11 color: 'gray92'
    
            top.geometry("198x121+250+151")
            top.minsize(116, 1)
            top.maxsize(1028, 750)
            top.resizable(1, 1)
            top.title("New Toplevel")
            top.configure(background="#d9d9d9")
    
            self.chkbtn_t1 = tk.Checkbutton(top)
            self.chkbtn_t1.place(relx=0.051, rely=0.165, relheight=0.215
                    , relwidth=0.313)
            self.chkbtn_t1.configure(activebackground="#ececec")
            self.chkbtn_t1.configure(activeforeground="#000000")
            self.chkbtn_t1.configure(background="#d9d9d9")
            self.chkbtn_t1.configure(disabledforeground="#a3a3a3")
            self.chkbtn_t1.configure(foreground="#000000")
            self.chkbtn_t1.configure(highlightbackground="#d9d9d9")
            self.chkbtn_t1.configure(highlightcolor="black")
            self.chkbtn_t1.configure(justify='left')
            self.chkbtn_t1.configure(text='''Apple''')
            self.chkbtn_t1.configure(variable=case_support.che43)
    
            self.btn_push = tk.Button(top, command=self.clearState)#######################################change
            self.btn_push.place(relx=0.505, rely=0.331, height=46, width=78)
            self.btn_push.configure(activebackground="#ececec")
            self.btn_push.configure(activeforeground="#000000")
            self.btn_push.configure(background="#d9d9d9")
            self.btn_push.configure(disabledforeground="#a3a3a3")
            self.btn_push.configure(foreground="#000000")
            self.btn_push.configure(highlightbackground="#d9d9d9")
            self.btn_push.configure(highlightcolor="black")
            self.btn_push.configure(pady="0")
            self.btn_push.configure(text='''Push''')
    
        def clearState(self):
            print("Test")
            case_support.che43.set(0)
            #self.chkbtn_t1.configure(variable=1)#######################################change
    
    if __name__ == '__main__':
        vp_start_gui()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

---
title: tkinter_plot_ui
date: 2020-05-07
---
Example Python program tkinter_plot_ui.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import matplotlib
* from numpy import arange, sin, pi
* from matplotlib.backends.backend_tkagg import FigureCanvasTkAgg
* from matplotlib.figure import Figure
* from matplotlib.backend_bases import key_press_handler
* # import matplotlib.animation as animation
* import sys
* import tkinter as Tk

## Methods

* def destroy(e):
* def on_key_event(event):
* def _quit():

## Code

Python tkinter example

    import matplotlib
    
    from numpy import arange, sin, pi
    from matplotlib.backends.backend_tkagg import FigureCanvasTkAgg
    from matplotlib.figure import Figure
    from matplotlib.backend_bases import key_press_handler
    # import matplotlib.animation as animation
    
    
    import sys
    import tkinter as Tk
    
    matplotlib.use('TkAgg')
    
    
    def destroy(e):
        sys.exit()
    
    
    root = Tk.Tk()
    root.wm_title("Embedding in TK")
    
    
    f = Figure(figsize=(5, 4), dpi=100)
    a = f.add_subplot(111)
    # t = arange(0.0, 3.0, 0.01)
    t = arange(0.0, 7.0, 0.01)
    # print(t)
    s = sin(2*pi*t)
    
    a.plot(t, s)
    a.set_title('Tk embedding')
    a.set_xlabel('X axis label')
    a.set_ylabel('Y label')
    # anim = animation.FuncAnimation(f, 5, interval=1000)
    
    # a tk.DrawingArea
    canvas = FigureCanvasTkAgg(f, master=root)
    # ## canvas.show()
    canvas.get_tk_widget().pack(side=Tk.TOP, fill=Tk.BOTH, expand=1)
    
    canvas._tkcanvas.pack(side=Tk.TOP, fill=Tk.BOTH, expand=1)
    
    # button = Tk.Button(master=root, text='Quit', command=sys.exit)
    # button.pack(side=Tk.BOTTOM)
    
    
    def on_key_event(event):
        print('you pressed %s' % event.key)
        # key_press_handler(event, canvas, toolbar)
        key_press_handler(event, canvas)
    
    
    def _quit():
        root.quit()     # stops mainloop
        root.destroy()  # this is necessary on Windows to prevent
        # Fatal Python Error: PyEval_RestoreThread: NULL tstate
    
    
    buttona = Tk.Button(master=root, text='Quit', command=_quit)
    buttonb = Tk.Button(master=root, text='Quit b', command=_quit)
    buttona.pack(side=Tk.BOTTOM)
    buttonb.pack(side=Tk.BOTTOM)
    
    canvas.mpl_connect('key_press_event', on_key_event)
    
    
    Tk.mainloop()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

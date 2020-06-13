---
title: embed_plt_in_tk
date: 2020-05-07
---
Example Python program embed_plt_in_tk.py

## Modules

* import matplotlib
* import numpy as np
* from matplotlib.backends.backend_tkagg import FigureCanvasTkAgg, NavigationToolbar2TkAgg
* from matplotlib.backend_bases import key_press_handler
* from matplotlib.figure import Figure
* import tkinter as Tk

## Methods

* def on_key_event(event):
* def _quit():

## Code

Python tkinter example

    # -*- coding: utf-8 -*-
    #!/usr/bin/env python
    
    import matplotlib
    matplotlib.use('TkAgg')
    
    import numpy as np
    from matplotlib.backends.backend_tkagg import FigureCanvasTkAgg, NavigationToolbar2TkAgg
    # implement the default mpl key bindings
    from matplotlib.backend_bases import key_press_handler
    from matplotlib.figure import Figure
    
    import tkinter as Tk
    
    root = Tk.Tk()
    root.wm_title("Embedding in TK")
    
    
    f = Figure(figsize=(5, 4), dpi=100)
    a = f.add_subplot(111)
    t = np.arange(0.0, 3.0, 0.01)
    s = np.sin(2*np.pi*t)
    
    a.plot(t, s)
    
    
    # tk.DrawingArea
    canvas = FigureCanvasTkAgg(f, master=root)
    canvas.show()
    canvas.get_tk_widget().pack(side=Tk.TOP, fill=Tk.BOTH, expand=1)
    
    toolbar = NavigationToolbar2TkAgg(canvas, root)
    toolbar.update()
    canvas._tkcanvas.pack(side=Tk.TOP, fill=Tk.BOTH, expand=1)
    
    def on_key_event(event):
        key_press_handler(event, canvas, toolbar)
    
    canvas.mpl_connect('key_press_event', on_key_event)
    
    def _quit():
        # stops mainloop
        root.quit()     
        root.destroy()
    
    button = Tk.Button(master=root, text='Quit', command=_quit)
    button.pack(side=Tk.BOTTOM)
    
    root.protocol("WM_DELETE_WINDOW", _quit)
    root.mainloop()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

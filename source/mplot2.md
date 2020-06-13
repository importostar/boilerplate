---
title: mplot2
date: 2020-05-07
---
Example Python program mplot2.py

## Modules

* vimport tkinter as tk 
* from tkinter import ttk
* import matplotlib
* from matplotlib.backends.backend_tkagg import FigureCanvasTkAgg, NavigationToolbar2TkAgg
* from matplotlib.figure import Figure
* from matplotlib.path import Path
* import matplotlib.patches as patches

## Code

Python tkinter example

    vimport tkinter as tk 
    from tkinter import ttk
    import matplotlib
    matplotlib.use("TkAgg")
    from matplotlib.backends.backend_tkagg import FigureCanvasTkAgg, NavigationToolbar2TkAgg
    from matplotlib.figure import Figure
    from matplotlib.path import Path
    import matplotlib.patches as patches
    
    win = tk.Tk()
    #plt.plot([1,2,3,4])
    #plt.ylabel('some numbers')
    verts = [
       (0., 0.),  # left, bottom
       (0., 1.),  # left, top
       (1., 1.),  # right, top
       (1., 0.),  # right, bottom
       (0., 0.),  # ignored
    ]
    
    codes = [
        Path.MOVETO,
        Path.LINETO,
        Path.LINETO,
        Path.LINETO,
        Path.CLOSEPOLY,
    ]
    
    path = Path(verts, codes)
    
    frame = ttk.Frame(win)
    f = Figure(figsize=(5,5), dpi=100)
    #a = f.add_subplot(111)
    #a.plot([1,2,3,4,5,6,7,8],[5,6,1,3,8,9,3,5])
    ax = f.add_subplot(111)
    patch = patches.PathPatch(path, facecolor='orange', lw=2)
    ax.add_patch(patch)
    ax.set_xlim(-2, 2)
    ax.set_ylim(-2, 2)
    
    canvas = FigureCanvasTkAgg(f, frame)
    canvas.show()
    canvas.get_tk_widget().pack(side=tk.BOTTOM, fill=tk.BOTH, expand=True)
    frame.pack()
    win.mainloop()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

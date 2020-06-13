---
title: matplotlib_frame_example (1)
date: 2020-05-07
---
Example Python program matplotlib_frame_example (1).py

## Modules

* import tkinter as Tk
* import matplotlib_frame
* from scipy import sin, cos, linspace, pi

## Methods

* def change_data():

## Code

Python tkinter example

    # An example showing how to use the GraphFrame class
    
    import tkinter as Tk
    import matplotlib_frame
    from scipy import sin, cos, linspace, pi
    
    # Create the root window
    root = Tk.Tk()
    
    # Create a GraphFrame and pack it inside of root
    gf = matplotlib_frame.GraphFrame(root, show_toolbar=True)
    gf.pack(side=Tk.TOP)
    
    # Plot two functions
    space = linspace(0, 4*pi, 100)
    gf.subplot.plot(space, cos(space))
    line, = gf.subplot.plot(space, sin(space))
    
    # Add a button for changing data
    def change_data():
        line.set_data(space, cos(space+pi/4))
        # Note that the canvas needs to be redrawn after a data change
        gf.draw()
    b = Tk.Button(root, text="Change data", command=change_data)
    b.pack()
    
    # Start the mainloop
    root.mainloop()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

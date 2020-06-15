---
title: pgf_subplot_ylabel_align_test (1)
date: 2020-05-07
---
Example Python program pgf_subplot_ylabel_align_test (1).py

## Modules

* from sys import argv
* import matplotlib
* import matplotlib.pyplot as plt
* import matplotlib.transforms as tfs
* import numpy as np

## Methods

* def align_ylabels(event):

## Code

Python example

    """
        +-----+                    +-----+
      a |     |                a   |     |
      x | ax1 |                x   | ax1 |
      1 |     |                1   |     |
        +-----+ should become:     +-----+
    a   |     |                a   |     |
    x   | ax2 |                x   | ax2 |
    2   |     |                2   |     |
        +-----+                    +-----+
    """
    
    from sys import argv
    
    # To avoid issue #2037, correct backend has to be loaded here
    import matplotlib
    if len(argv) > 1:
        matplotlib.use('pgf')
    else:
        matplotlib.use('Agg')
    import matplotlib.pyplot as plt
    import matplotlib.transforms as tfs
    import numpy as np
    
    
    def align_ylabels(event):
        fig = event.canvas.figure
        axes = fig.axes
        # Get desired (=smallest) x value
        xpos = min(ax.yaxis.get_label().get_position()[0] for ax in axes)
        for ax in axes:
            # get_position() returns xpos in display coordinates and ypos in
            # axes coordinates, this transform accounts for that
            trans = tfs.blended_transform_factory(tfs.IdentityTransform(), ax.transAxes)
            # Update label coordinates
            ax.yaxis.set_label_coords(xpos, 0.5, transform=trans)
        # Following tidbit stolen from http://stackoverflow.com/a/4056853/1145828
        # Remove callbacks before redrawing figure with updated coordinates,
        # to avoid recursion
        func_handles = fig.canvas.callbacks.callbacks[event.name]
        fig.canvas.callbacks.callbacks[event.name] = {}
        # Redraw figure
        fig.canvas.draw()
        # Reset callbacks
        fig.canvas.callbacks.callbacks[event.name] = func_handles
    
    
    f = plt.figure()
    f.canvas.mpl_connect('draw_event', align_ylabels)
    
    ax1 = f.add_subplot(211, ylabel='ax1')
    ax2 = f.add_subplot(212, ylabel='ax2')
    
    # y1 and y2 are of different width so the top and bottom labels are
    # intentionally misaligned
    x = np.linspace(0, 10)
    y1 = np.linspace(0, 10)
    y2 = np.linspace(1000, 10000)
    
    ax1.plot(x, y1)
    ax2.plot(x, y2)
    
    if len(argv) > 1:
        # Use PGF backend to save PDF file
        # ylabel alignment doesn't work
        f.savefig('img.pdf')
    else:
        # Use Agg backend to save PNG file
        # ylabel alignment works
        f.savefig('img.png')
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

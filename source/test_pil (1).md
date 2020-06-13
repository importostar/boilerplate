---
title: test_pil (1)
date: 2020-05-07
---
Example Python program test_pil (1).py
For Python version 2.x.
To test your Python version use:

    python --version

## Modules

* import matplotlib
* import numpy as np
* import matplotlib.pyplot as plt
* from matplotlib.collections import LineCollection
* from PIL import Image, ImageDraw, ImageTk
* import Tkinter as tk
* import time

## Methods

* def plot(t, spikes, size):
* def show():

## Code

Python tkinter example

    #!/usr/bin/env python
    #coding=utf-8
    
    import matplotlib
    #matplotlib.rcParams.update({'lines.antialiased': False})
    matplotlib.use('MacOSX')
    import numpy as np
    import matplotlib.pyplot as plt
    from matplotlib.collections import LineCollection
    from PIL import Image, ImageDraw, ImageTk
    import Tkinter as tk
    
    im = Image.new('RGBA', (800, 600))
    draw=ImageDraw.Draw(im)
    
    root= tk.Tk()
    
    def plot(t, spikes, size):
    
        nx, ny = size
        ts, ns = spikes.shape
        xmin, xmax = t.min(), t.max()
        ymin, ymax = spikes.min(), spikes.max()
    
        spikes = (1-(spikes-ymin)/(ymax-ymin))*ny
        t = (t-xmin)/(xmax-xmin)*nx
    
        segs = np.empty((ns, ts, 2), np.float32)
        segs[:, :, 1] = spikes.T
        segs[:, :, 0] = t[:, None].T
        
        for i in xrange(ns):
            draw.line(segs[i,:,:])
    
    def show():
        root.tkIm = ImageTk.PhotoImage(im)
        root.label_image = tk.Label(root, image=root.tkIm)
        root.label_image.pack()
        root.update()
    
    t = np.linspace(0, np.pi*2, 34)
    y = np.sin(t) 
    spikes = y[:, None]*np.random.rand(1,50000)
    
    import time
    
    start1 = time.time()
    #plt.plot(t, spikes, '-')
    plot(t, spikes, (800, 600))
    start2 = time.time()
    show()
    stop = time.time()
    print 'Plotting:', -start1+start2 
    print 'Exporting:', -start2+stop
    print 'total:', -start1+stop
    root.mainloop()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

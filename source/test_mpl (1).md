---
title: test_mpl (1)
date: 2020-05-07
---
Example Python program test_mpl (1).py
For Python version 2.x.
To test your Python version use:

    python --version

## Modules

* import matplotlib
* import numpy as np
* import matplotlib.pyplot as plt
* from matplotlib.collections import LineCollection
* import time

## Methods

* def line_collection(t, spikes):

## Code

Python example

    #!/usr/bin/env python
    #coding=utf-8
    
    import matplotlib
    #matplotlib.rcParams.update({'lines.antialiased': False})
    import numpy as np
    import matplotlib.pyplot as plt
    from matplotlib.collections import LineCollection
    
    def line_collection(t, spikes):
    
        ax = plt.subplot(111)
        ts, ns = spikes.shape
        segs = np.zeros((ns, ts, 2), np.float32)
        segs[:, :, 1] = spikes.T
        segs[:, :, 0] = t[:, None].T
    
        line_segments = LineCollection(segs)
    
        ax.add_collection(line_segments)
        
        ax.set_xlim(t.min(), t.max())
        ax.set_ylim(spikes.min(), spikes.max())
        
    
    
    
    t = np.linspace(0, np.pi*2, 34)
    y = np.sin(t) 
    spikes = y[:, None]*np.random.rand(1,50000)
    
    import time
    
    start1 = time.time()
    #plt.plot(t, spikes, '-')
    line_collection(t, spikes)
    start2 = time.time()
    plt.savefig('plot_perf.png')
    stop = time.time()
    print 'Plotting:', -start1+start2 
    print 'Exporting:', -start2+stop
    print 'total:', -start1+stop
    print matplotlib.get_backend()
    plt.show()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

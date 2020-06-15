---
title: wall crossing
date: 2020-05-07
---
Example Python program wall-crossing.py
For Python version 2.x.
To test your Python version use:

    python --version

## Modules

* import numpy as np
* import matplotlib.pyplot as plt

## Code

Python example

    # plt.contour assumes there are lines between theta = 0 and theta = 2*np.pi
    
    import numpy as np
    import matplotlib.pyplot as plt
    #%matplotlib inline
    plt.rcParams['figure.figsize']=7,7
    
    # rm foo*.png
    # convert foo*.png foo.gif
    
    dt = 0.01
    L = 5
    t  = np.arange(-L,L+dt, dt)
    z = t[...,None]+1j*t[None,...]
    
    N = 20
    
    PP = np.polyval(P,z)
    
    for k in np.arange(N):
        print "%02d" %(k)
    
        w = np.log(np.exp(2j*np.pi*(k*1.0/N))*PP)
    
        ds = 0.05
        plt.contour(t, t, w.imag%(2*np.pi), levels = 2*np.pi*np.arange(0,1, ds), colors=('#505050','#707070'), linewidth=1)
        plt.contour(t, t, w.imag%(2*np.pi), levels = 2*np.pi*np.arange(0,1, 0.5), colors='w', linewidth=50)
        plt.contour(t, t, w.real, levels = np.arange(0,5,0.1)**1, colors=('#A2D426','#6B6CED'))
    
        L = 3
        plt.xlim([-L,L])
        plt.ylim([-L,L])
        #plt.show()
    
        plt.savefig('/home/jdm/Documents/math/foo-%02d.png'%(k))
        plt.clf()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

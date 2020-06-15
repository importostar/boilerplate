---
title: contact_code1
date: 2020-05-07
---
Example Python program contact_code1.py

## Modules

* from mpl_toolkits.mplot3d import Axes3D
* from matplotlib import *
* from matplotlib import cm
* from matplotlib.ticker import LinearLocator, FormatStrFormatter
* import matplotlib.pyplot as plt
* import numpy as np
* import sys
* from pylab import *

## Code

Python example

    from mpl_toolkits.mplot3d import Axes3D
    from matplotlib import *
    from matplotlib import cm
    from matplotlib.ticker import LinearLocator, FormatStrFormatter
    import matplotlib.pyplot as plt
    import numpy as np
    import sys
    from pylab import *
     
    rcParams['legend.loc'] = 'best'
     
    ae = 10
    be = 4
    pe = 101
    ne = 0.5
     
    xe = linspace(0,10)
    ye = linspace(0,4)
     
    ge1 = p * (1-((xe/ae)**2)-((0/be)**2))**0.5
    ge2 = p * (1-((0/ae)**2)-((ye/be)**2))**0.5
     
    fig = plt.figure()
    axe = fig.add_subplot(111)
     
    plot(xe,ge1, label='major axis')
    plot(ye,ge2, label='minor axis')
    legend()
    font = {'fontname':'Times New Roman}','fontsize':'16'}
     
    axe.set_xlabel('Distance from centre of contact (mm)', **font)
    axe.set_ylabel('Contact Pressure (MPa)', **font)
    axe.grid(True)
     
    plt.show()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

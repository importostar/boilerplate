---
title: IpythonOnlineUpdate
date: 2020-05-07
---
Example Python program IpythonOnlineUpdate.py

## Modules

* import time
* import math
* import pylab as plt
* from IPython import display
* from matplotlib import colors as mcolors

## Code

Python example

    %matplotlib inline
    import time
    import math
    import pylab as plt
    from IPython import display
    from matplotlib import colors as mcolors
    
    m = (math.sqrt(5)+1)/2.0
    #m = math.sqrt(2.0)
    
    
    xx = []
    yy = []
    rr = []
    plt.figure(figsize=(7,7))
    colors = {i:c for i,c in enumerate(mcolors.CSS4_COLORS)}
    colors = list('kbcygmrw')
    for t in range(1500):
        r = (t*m) // (2*math.pi)
        rr.append(r)
        yy.append(r*math.sin(t*m))
        xx.append(r*math.cos(t*m))
        
        li = min(xx+yy)
        lu = max(xx+yy)
        
        lu = max(abs(li), abs(lu)) *1.1    
        li = -lu
        
        if t % 15 > 0:
            continue;
        
        plt.clf()
        plt.axis('off');
        plt.xlim((li,lu))
        plt.ylim((li,lu))
        plt.plot(xx,yy, alpha=0.25);
        plt.scatter(xx,yy, alpha=0.7,c=[colors[int(r%len(colors))] for r in rr]);
        display.display(plt.gcf())
        display.clear_output(wait=True)
        time.sleep(0.0001)

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

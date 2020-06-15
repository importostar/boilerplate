---
title: burst plot
date: 2020-05-07
---
Example Python program burst-plot.py

## Modules

* import numpy.random as nr
* import matplotlib.pyplot as mp

## Methods

* def burst(span, bypriority, bufsize):
* def maxindex(l):

## Code

Python example

    import numpy.random as nr
    import matplotlib.pyplot as mp
    
    def burst(span, bypriority, bufsize):
        result = []
        #rands = nr.rand(bufsize + span)
        rands = nr.randn(bufsize + span)
        buf = [(w, -1) for w in rands[:bufsize]]
        for time, w in enumerate(rands[bufsize:]):
            well = nr.rand() < bypriority
            i = maxindex(buf) if well else nr.randint(0, bufsize)
            result.append(time - buf[i][1])
            #if well: result.append(time - buf[i][1])
            buf[i] = (w, time)
            pass
        return result
    
    def maxindex(l):
        k, m = 0, l[0]
        for i, v in enumerate(l[1:]):
            if v >= m: k, m = i, v
            pass
        return k
    
    
    data = burst(10000, 0.5, 7)
    mp.figure()
    mp.hist(data, 128, (0, 128))
    mp.figure()
    mp.hist(data, 128, (0, 128), log=True)
    mp.show()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

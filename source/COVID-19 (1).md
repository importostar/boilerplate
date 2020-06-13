---
title: COVID 19 (1)
date: 2020-05-07
---
Example Python program COVID-19 (1).py

## Modules

* import numpy, scipy.integrate, matplotlib.pyplot

## Methods

* def ds(x, y, z, a, b, c, d, e):
* def dr(x, y, z, a, b, c, d, e):
* def dd(x, y, z, a, b, c, d, e):
* def dv(t, vec, a, b, c, d, e):
* def plot(transm):

## Code

Python example

    import numpy, scipy.integrate, matplotlib.pyplot
    
    
    pop = 300000000.0
    recovery = 0.2
    badreco = 0.005
    death = 0.001
    contact = 0.3
    
    sick = 30000.0
    dead = 0.0
    recovered = 0.0
    
    
    def ds(x, y, z, a, b, c, d, e):
        return sum([b * x * (a - x - z - y) / a, -x * e, -x * c, -x * d])
    
    
    def dr(x, y, z, a, b, c, d, e):
        return x * e
    
    
    def dd(x, y, z, a, b, c, d, e):
        return x * c
    
    
    def dv(t, vec, a, b, c, d, e):
        return ds(*vec, a, b, c, d, e), dd(*vec, a, b, c, d, e), dr(*vec, a, b, c, d, e)
    
    
    times = numpy.linspace(0, 360, 361)
    
    
    def plot(transm):
        matplotlib.pyplot.clf()
        solution = scipy.integrate.odeint(dv, (sick, dead, recovered), times, tfirst=True, args=(pop, transm, death, badreco, recovery))
        matplotlib.pyplot.plot(times, solution[:, 0], "b", label="Sick")
        matplotlib.pyplot.plot(times, solution[:, 1], "r", label="Deaths")
        matplotlib.pyplot.plot(times, solution[:, 2], "g", label="Recovered")
        matplotlib.pyplot.legend(loc="best")
    
    
    plot(contact)
    
    
    matplotlib.pyplot.xlabel("Days")
    matplotlib.pyplot.ylabel("Cases")
    
    
    matplotlib.pyplot.show()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

---
title: gistfile1 (1)
date: 2020-05-07
---
Example Python program gistfile1 (1).py

## Modules

* import numpy as np
* import matplotlib.pyplot as plt
* import math

## Code

Python example

    import numpy as np
    import matplotlib.pyplot as plt
    import math
    
    
    periode = 2*math.pi/math.sqrt(10)
    frekvens = 1/periode
    
    # sekunder 
    sek = 4*periode
    
    #steps
    N = 10000
    N2 = 1000
    
    t = np.linspace(0, sek, N)
    
    k = 0.1
    m = 0.01
    
    x = np.zeros(N)
    v = np.zeros(N)
    a = np.zeros(N)
    
    x[0] = 0.01
    v[0] = 0.05
    
    a = -k*x[0]/m
    
    for i in range(1, N):
        x[i] = x[i-1] + v[i-1] * (sek/N)
        v[i] = v[i-1] + a * (sek/N)
        a = -k*x[i]/m
    
    t2 = np.linspace(0,sek, N2)
    x2 = np.zeros(N2)
    
    for i in range(0,N2):
        x2[i] = 0.019*math.cos(math.sqrt(10) * i*sek/N2 - 1 )
    
    
    plt.xlabel("Sekunder/s")
    plt.ylabel("Posisjon/m")
    plt.title("10000 steps")
    plt.ylim(-0.025, 0.025)
    
    plt.plot(t2,x2)
    plt.plot(t,x)
    plt.savefig("10000steps.png")
    plt.show()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

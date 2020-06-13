---
title: run_2
date: 2020-05-07
---
Example Python program run_2.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import matplotlib.pyplot as plt
* import matplotlib
* import matplotlib.ticker as ticker
* from matplotlib import rc
* import numpy as np
* import math

## Code

Python example

    # Random Walker ThP4 14.Mai 2020
    # Quentin Wach
    import matplotlib.pyplot as plt
    import matplotlib
    import matplotlib.ticker as ticker
    from matplotlib import rc
    rc('font',**{'family':'sans-serif','sans-serif':['Helvetica']})
    rc('text', usetex=True)
    import numpy as np
    import math
    np.random.seed(14520)
    
    # Figure Setup
    matplotlib.style.use('ggplot')
    fig, ax = plt.subplots(1, figsize=(6,2.7), dpi=300)
    
    # Parameter
    P = 0.3               # Schritt nach Links
    Q = 1 - P             # Schritt nach Rechts
    T = (10,100,1000)     # Schritte
    V = 10000              # Versuche pro Experiment
    
    # Experimente
    for t in T:
    
        # Endpunkte [Schritte]
        X = []
        for v in range(V):
            x = 0       # Startpunkt
            l_step = "" # letzter Schritt
            for i in range(t):
                if l_step == "":
                    if np.random.random_sample() <= P:
                        x -= 1
                        l_step = "L"
                    else:
                        x += 1
                        l_step = "R"
                else:
                    if l_step == "L":
                        if np.random.random_sample() <= 0.8:
                            x -= 1
                            l_step = "L"
                        else:
                            x += 1
                            l_step = "R"
    
                    if l_step =="R":
                        if np.random.random_sample() <= 0.6:
                            x -= 1
                            l_step = "L"
                        else:
                            x += 1
                            l_step = "R"
    
            X.append(x)
        X = sorted(X)
        
        # Wahrscheinlichkeiten
        Y = []
        for x in X:
            Y.append(X.count(x)/len(X))
    
        # Histogramm
        ax.fill_between(X, Y, facecolor='black', step="mid", zorder=30)
    
        # entferne Überflüssige Daten (besser wäre, sie zu mitteln)
        new_X = []; new_Y = []
        for x in X:
            if x not in new_X:
                new_X.append(x)
                new_Y.append(Y[X.index(x)])
    
        # Shannon-Information
        I = 0
        for y in new_Y:
            I += y * math.log(y, np.e)
        print(I)
    
    
    # Axes & Grid
    ax.set_ylim(0,0.14)
    ax.xaxis.set_major_locator(ticker.MultipleLocator(50))
    ax.xaxis.set_minor_locator(ticker.MultipleLocator(10))
    ax.grid(b=True, color='white', linestyle="--", linewidth=0.5, zorder=0)
    
    # Label & Text
    plt.ylabel("Wahrscheinlichkeit", size=9)
    plt.xlabel(r"Schritte $x$", size=9)
    plt.text(-140, 0.121, r"$P_1[x(t=10)]$")
    plt.text(-175, 0.05, r"$P_2[x(t=100)]$")
    plt.text(-600, 0.025, r"$P_3[x(t=1000)]$")
    
    # Render
    plt.tight_layout()
    plt.savefig("Abb_2.png", bbox_inches="tight")

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

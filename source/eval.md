---
title: eval
date: 2020-05-07
---
Example Python program eval.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import matplotlib.pyplot as plt
* import numpy as np
* import pandas
* from scipy.stats import mannwhitneyu
* from scipy import stats
* from a12 import *
* from Tkinter import *   ## notice capitalized T in Tkinter 
* from tkinter import *   ## notice lowercase 't' in tkinter here

## Code

Python tkinter example

    #!/usr/bin/env python3
    import matplotlib.pyplot as plt
    import numpy as np
    import pandas
    from scipy.stats import mannwhitneyu
    from scipy import stats
    from a12 import *
    
    try:
            # for Python2
                from Tkinter import *   ## notice capitalized T in Tkinter 
    except ImportError:
            # for Python3
                from tkinter import *   ## notice lowercase 't' in tkinter here
    
    data = {}
    
    for key in ["baseline", "exp1", "exp2", "exp3"]:
        with open("fuzz-{}.log".format(key)) as fp:
            data[key] = []
            for line in fp:
                data[key].extend([int(x) for x in line.split()])
            ## Basic stats
            print("Basic stats for {}".format(key))
            print(stats.describe(data[key]))
    
    print("MW U Baseline vs. Exp1")
    print(mannwhitneyu(data["baseline"], data["exp1"]))
    print("MW U Baseline vs. Exp2")
    print(mannwhitneyu(data["baseline"], data["exp2"]))
    print("MW U Baseline vs. Exp3")
    print(mannwhitneyu(data["baseline"], data["exp3"]))
    
    print("MW U Exp1 vs. Exp2")
    print(mannwhitneyu(data["exp1"], data["exp2"]))
    print("MW U Exp1 vs. Exp3")
    print(mannwhitneyu(data["exp1"], data["exp3"]))
    
    print("MW U Exp2 vs. Exp3")
    print(mannwhitneyu(data["exp2"], data["exp3"]))
    
    
    ## A12 statistic
    baseline = ["baseline"]
    baseline.extend(data["baseline"])
    
    exp1 = ["exp1"]
    exp1.extend(data["exp1"])
    
    exp2 = ["exp2"]
    exp2.extend(data["exp2"])
    
    exp3 = ["exp3"]
    exp3.extend(data["exp3"])
    
    rxs = [baseline,exp1,exp2,exp3]
    print("A12 over 0.56")
    for rx in a12s(rxs,enough=0.56): print(rx)
    print("A12 over 0.64")
    for rx in a12s(rxs,enough=0.64): print(rx)
    print("A12 over 0.71")
    for rx in a12s(rxs,enough=0.71): print(rx)
    
    ## Plots
    pltd = [data["baseline"], data["exp1"], data["exp2"], data["exp3"]]
    # multiple box plots on one figure
    plt.figure()
    plt.boxplot(pltd)
    plt.xticks([1, 2, 3, 4], ['Baseline (No Dict)', 'Dict A', 'Dict B', 'Dict C'])
    plt.ylabel("Coverage (Num. PCs)")
    plt.savefig("Coverage box plots", dpi=150)

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

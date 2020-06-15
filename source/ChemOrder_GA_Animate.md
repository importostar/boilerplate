---
title: ChemOrder_GA_Animate
date: 2020-05-07
---
Example Python program ChemOrder_GA_Animate.py

## Modules

* import numpy as np
* import subprocess
* import matplotlib
* import matplotlib.pyplot as plt
* import matplotlib.cm as cm
* from ase.db import connect

## Code

Python example

    """Animate results from a GA search for chemical ordering optimization in
    nanoparticles. Assumes http://www.imagemagick.org/ has been installed."""
    import numpy as np
    import subprocess
    import matplotlib
    import matplotlib.pyplot as plt
    import matplotlib.cm as cm
    
    from ase.db import connect
    
    matplotlib.rc('font', serif='Helvetica Neue Light')
    matplotlib.rcParams.update({'font.size': 22})
    
    db = connect('gadb.db')
    
    energy = []
    mass = []
    index = []
    i = 0
    for row in db.select(relaxed=True):
        i += 1
        c = row.toatoms(add_additional_information=True)
        energy.append(c.info['key_value_pairs']['raw_score'] * -1.)
        mass.append(round(sum(c.get_masses()), 2))
        index.append(i)
    
    cenergy, cmass, cindex = [], [], []
    fname = []
    for i in range(len(index)):
        cenergy.append(energy[i])
        cmass.append(mass[i])
        cindex.append(index[i])
    
        fig = plt.figure(figsize=(12, 12))
        ax = fig.add_subplot(111)
        ax.axis([min(mass)-10, max(mass)+10, -5.5, 5.5])
        ax.scatter(cmass, cenergy, c=cindex, cmap=cm.rainbow, alpha=0.5)
        plt.xlabel('Mass')
        plt.ylabel('Stability (eV)')
    
        n = 'images/{0}_gaPtAu.png'.format(i)
        fname.append(n)
        fig.savefig(n)
    
    call = 'convert -delay 15 -loop 0 '
    for i in fname:
        call += i + ' '
    call += 'images/animated.gif'
    
    subprocess.call(call, shell=True)
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

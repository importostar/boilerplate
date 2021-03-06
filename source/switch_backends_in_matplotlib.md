---
title: switch_backends_in_matplotlib
date: 2020-05-07
---
Example Python program switch_backends_in_matplotlib.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import matplotlib
* from matplotlib import pyplot as plt
* import matplotlib
* from matplotlib import pyplot as plt

## Code

Python example

    # This file was obtained from StackOverflow:
    #
    # How to switch backends in matplotlib / Python
    # https://stackoverflow.com/questions/3285193/how-to-switch-backends-in-matplotlib-python
    
    
    import matplotlib
    gui_env = ['TKAgg','GTKAgg','Qt4Agg','WXAgg']
    for gui in gui_env:
        try:
            print("testing", gui)
            matplotlib.use(gui,warn=False, force=True)
            from matplotlib import pyplot as plt
            break
        except:
            continue
    print("Using:",matplotlib.get_backend())
    
    
    import matplotlib
    gui_env = [i for i in matplotlib.rcsetup.interactive_bk]
    non_gui_backends = matplotlib.rcsetup.non_interactive_bk
    print ("Non Gui backends are:", non_gui_backends)
    print ("Gui backends I will test for", gui_env)
    for gui in gui_env:
        print ("testing", gui)
        try:
            matplotlib.use(gui,warn=False, force=True)
            from matplotlib import pyplot as plt
            print ("    ",gui, "Is Available")
            plt.plot([1.5,2.0,2.5])
            fig = plt.gcf()
            fig.suptitle(gui)
            plt.show()
            print ("Using ..... ",matplotlib.get_backend())
        except:
            print ("    ",gui, "Not found")

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

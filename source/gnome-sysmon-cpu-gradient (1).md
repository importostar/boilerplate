---
title: gnome sysmon cpu gradient (1)
date: 2020-05-07
---
Example Python program gnome-sysmon-cpu-gradient (1).py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import argparse
* from matplotlib.colors import to_hex
* from matplotlib.pyplot import get_cmap
* from matplotlib.cm import cmap_d
* from numpy import linspace

## Code

Python example

    import argparse
    from matplotlib.colors import to_hex
    from matplotlib.pyplot import get_cmap
    from matplotlib.cm import cmap_d
    from numpy import linspace
    
    parser = argparse.ArgumentParser(
        description='Generate color gradient for GNOME System Monitor. '
        'Can be set at dconf key /org/gnome/gnome-system-monitor/cpu-colors'
    )
    parser.add_argument('cores', help='number of cores', type=int)
    parser.add_argument('--colormap', help=f'matplotlib colormap: {list(cmap_d.keys())}', default='rainbow', type=str)
    parser.add_argument('--start', help="colormap start value (between 0 and 1)", default=0.0, type=float)
    parser.add_argument('--end', help="colormap end value (between 0 and 1)", default=1.0, type=float)
    
    if __name__=="__main__":
        args = parser.parse_args()
    
        # Choose a colormap from https://matplotlib.org/3.1.0/tutorials/colors/colormaps.html
        map = get_cmap(args.colormap)
    
        # Start/end values to select part of the colormap.
        #   The first color in the gradient will always be visible in the graph
        #   -> e.g.: for 'rainbow' I set the extent to [0.2, 1] to make the first color blue instead of purple
        cpu_colors = [
            (i, to_hex(map(value)))
            for i,value in enumerate(linspace(args.start,args.end,args.cores))
        ]
    
        print(cpu_colors)
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

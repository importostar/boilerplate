---
title: ssce
date: 2020-05-07
---
Example Python program ssce.py

## Modules

* import matplotlib
* import holoviews as hv

## Code

Python tkinter example

    #!/usr/bin/env python
    # -*- coding: utf-8 -*-
    
    import matplotlib
    matplotlib.use('agg') # avoid use of tkinter (not preinstalled on Linux)
    # GIF support requires ImageMagick which is installed by default on many Linux installations
    import holoviews as hv
    hv.extension('matplotlib')
    
    # create a series of 5 x 5 heatmaps
    numHeatMaps = 2
    measurements = [[(i + 1, j + 1, k * 100 + i * 10 + j) for i in range(5) for j in range(5)] for k in range(numHeatMaps)]
    heatMapDict = {k:hv.HeatMap(measurements[k]) for k in range(len(measurements))}
    holo = hv.HoloMap(heatMapDict, kdims='index')
    
    # render the heatmaps as an animated GIF
    renderer = hv.renderer('matplotlib')
    renderer.fps = 5
    renderer.save(holo, 'holo', fmt='gif') # broken in Python 3.7 under Windows 10 for any value of numHeatMaps
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

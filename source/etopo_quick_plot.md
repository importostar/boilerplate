---
title: etopo_quick_plot
date: 2020-05-07
---
Example Python program etopo_quick_plot.py

## Modules

* import os
* from netCDF4 import Dataset
* import matplotlib.pyplot as plt
* import matplotlib.cm
* import numpy as np

## Methods

* def LevelColormap(levels, cmap=None):
* def etopoplotter(etopofile):

## Code

Python example

    #    hacked up from: http://www.trondkristiansen.com/?page_id=846
    
    import os
    from netCDF4 import Dataset
    import matplotlib.pyplot as plt
    import matplotlib.cm
    import numpy as np
    
    def LevelColormap(levels, cmap=None):
        """
        Make a colormap based on an increasing sequence of levels
        
        Notes
        --
        hacked up from: http://www.trondkristiansen.com/?page_id=846
        """
        # Start with an existing colormap
        if cmap == None:
            cmap = plt.get_cmap()
    
        # Spread the colours maximally
        nlev = len(levels)
        S = np.arange(nlev, dtype='float')/(nlev-1)
        A = cmap(S)
    
        # Normalize the levels to interval [0,1]
        levels = np.array(levels, dtype='float')
        L = (levels-levels[0])/(levels[-1]-levels[0])
    
        # Make the colour dictionary
        R = [(L[i], A[i,0], A[i,0]) for i in xrange(nlev)]
        G = [(L[i], A[i,1], A[i,1]) for i in xrange(nlev)]
        B = [(L[i], A[i,2], A[i,2]) for i in xrange(nlev)]
        cdict = dict(red=tuple(R),green=tuple(G),blue=tuple(B))
    
        # Use 
        return matplotlib.colors.LinearSegmentedColormap(
            '%s_levels' % cmap.name, cdict, 256)
    
    def etopoplotter(etopofile):
        """subset of etopo file
    
        Notes
        --
        hacked up from: http://www.trondkristiansen.com/?page_id=846
    
        Subset of complete dataset taken with: history = "Thu Jul 06 10:28:57 2017: cdo sellonlatbox,90,305,-60,5 ETOPO1_Bed_g_gmt4.grd test.nc"
        
        :etopofile: @todo
        :returns: @todo
        """
    
        ifile=Dataset(etopofile, 'r')
        x=ifile.variables['x'][:]
        y=ifile.variables['y'][:]
        bathy=ifile.variables['z'][:]
        levels=[-6000,-5000,-3000, -2000, -1500, -1000,-500, -400, -300, -250, -200, -150, -100, -75, -65, -50, -35, -25, -15, -10, -5, 0]
        cs1=plt.contourf(x,y,bathy,levels,cmap=LevelColormap(levels,cmap=matplotlib.cm.Blues_r),extend='both')
        cs1.cmap.set_over('#858588')
        plt.colorbar(cs1,orientation='vertical')
    
        plt.show()
    
    etopofile='/home/chris/mount_win/bathy/ETOPO_australia_crop.nc'
    etopoplotter(etopofile)
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

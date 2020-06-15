---
title: netcdf_basics
date: 2020-05-07
---
Example Python program netcdf_basics.py

## Modules

* import sys,getopt
* #from netCDF4 import Dataset  # use scipy instead
* from scipy.io import netcdf #### <--- This is the library to import.
* import matplotlib
* import matplotlib.pyplot as plt
* import numpy as np
* import os
* from datetime import datetime, timedelta
* import coltbls as coltbls
* from mpl_toolkits.basemap import Basemap
* from matplotlib.colors import LinearSegmentedColormap
* from mpl_toolkits.axes_grid import make_axes_locatable
* import matplotlib.axes as maxes

## Code

Python example

    import sys,getopt
    #from netCDF4 import Dataset  # use scipy instead
    from scipy.io import netcdf #### <--- This is the library to import.
    import matplotlib
    import matplotlib.pyplot as plt
    import numpy as np
    import os
    from datetime import datetime, timedelta
    import coltbls as coltbls
    from mpl_toolkits.basemap import Basemap
    from matplotlib.colors import LinearSegmentedColormap
    from mpl_toolkits.axes_grid import make_axes_locatable
    import matplotlib.axes as maxes
    
    
    # Running Script example:
    # $ python my_WRF_map.py wrfout_d0x_YYYY-MM-DD_HH:MM:SS
    
    # Open file in a netCDF reader
    directory = './'
    wrf_file_name = directory+'W0NQXP~N' #NC files are named funny in a windows system
    nc = netcdf.netcdf_file(wrf_file_name,'r')
    
    #Look at the variables available
    nc.variables
    
    #Look at the dimensions
    nc.dimensions
    
    #Look at a specific variable's dimensions
    nc.variables['T2'].dimensions   ## output is ('Time', 'south_north', 'west_east')
    
    #Look at a specific variable's units
    nc.variables['T2'].units        ## output is ('K')
    
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

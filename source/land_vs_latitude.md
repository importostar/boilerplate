---
title: land_vs_latitude
date: 2020-05-07
---
Example Python program land_vs_latitude.py
For Python version 2.x.
To test your Python version use:

    python --version

## Modules

* import cartopy
* import matplotlib
* import matplotlib.pyplot
* import numpy
* import shapely
* import pyguymer

## Code

Python example

    #!/usr/bin/env python2
    # -*- coding: utf-8 -*-
    
    # Import modules ...
    # NOTE: https://matplotlib.org/gallery/user_interfaces/canvasagg.html
    import cartopy
    import matplotlib
    matplotlib.use("Agg")
    import matplotlib.pyplot
    import numpy
    import shapely
    
    # Import my module ...
    try:
        import pyguymer
    except:
        raise Exception("you need to have the Python module from https://github.com/Guymer/PyGuymer located somewhere in your $PYTHONPATH")
    
    # Create latitudes and array to hold results ...
    lats = numpy.linspace(90.0, -90.0, num = 181)                                   # [deg]
    lands = numpy.zeros(lats.size, dtype = numpy.float64)                           # [deg]
    
    # Create plot and make it pretty ...
    fig = matplotlib.pyplot.figure(
        figsize = (9, 6),
            dpi = 300
    )
    ax = matplotlib.pyplot.axes(projection = cartopy.crs.Robinson())
    ax.set_global()
    pyguymer.add_map_background(ax, resolution = "large4096px")
    ax.coastlines(resolution = "10m", color = "black", linewidth = 0.1)
    
    # Find file containing all the country shapes ...
    shape_file = cartopy.io.shapereader.natural_earth(
        resolution = "10m",
        category = "cultural",
        name = "admin_0_countries"
    )
    
    # Loop over latitudes ...
    for i in xrange(lats.size):
        # Catch the special cases of the poles ...
        if i == 0:
            lands[i] = 0.0                                                          # [deg]
            continue
        if i == lats.size - 1:
            lands[i] = 360.0                                                        # [deg]
            continue
    
        # Make grid line ...
        # HACK: Some of the regions go past 180 degrees (presumably due to
        #       floating-point rounding errors) so the grid line has to wrap around
        #       to ensure that it crosses at the anti-meridian.
        grid_line = shapely.geometry.LineString(
            [
                (-181.0, lats[i]),
                ( 181.0, lats[i])
            ]
        )
    
        # Plot grid line ...
        matplotlib.pyplot.plot(
            [-180.0, 180.0],
            [lats[i], lats[i]],
            transform = cartopy.crs.PlateCarree(),
            color = "blue",
            linewidth = 0.1
        )
    
        # Make stack of longitudes ...
        lons = numpy.empty(0, dtype = numpy.float64)                                # [deg]
    
        # Loop over records ...
        for record in cartopy.io.shapereader.Reader(shape_file).records():
            # Loop over boundaries ...
            for boundary in record.geometry.boundary:
                # Find intersection of boundary with grid line ...
                tmp = boundary.intersection(grid_line)
    
                # Skip this intersection if it is empty ...
                if tmp.is_empty:
                    continue
    
                # Check that a sensible number of intersections have been found ...
                if len(tmp) % 2 == 1:
                    print "WARNING: An odd number of intersections was found at {0:.1f} (n = {1:d})".format(lats[i], len(tmp))
    
                    # Loop over parts ...
                    for part in tmp:
                        # Loop over coordinates ...
                        for coord in part.coords:
                            # Extract coordinates and add to stack ...
                            lon, lat = coord                                        # [deg], [deg]
    
                            # Add location to plot ...
                            matplotlib.pyplot.plot(
                                lon,
                                lat,
                                transform = cartopy.crs.PlateCarree(),
                                marker = "o",
                                markersize = 1.0,
                                markeredgewidth = 0.0,
                                color = "green"
                            )
                else:
                    # Loop over parts ...
                    for part in tmp:
                        # Loop over coordinates ...
                        for coord in part.coords:
                            # Extract coordinates and add to stack ...
                            lon, lat = coord                                        # [deg], [deg]
                            lons = numpy.append(lons, lon)                          # [deg]
    
        # Skip if there aren't any intersections ...
        if lons.size == 0:
            continue
    
        # Sort array ...
        lons.sort()
    
        # Loop over longitude pairs ...
        for j in xrange(0, lons.size, 2):
            # Add length to total ...
            lands[i] += (lons[j + 1] - lons[j])                                     # [deg]
    
            # Plot length ...
            matplotlib.pyplot.plot(
                [lons[j], lons[j + 1]],
                [lats[i], lats[i]],
                transform = cartopy.crs.PlateCarree(),
                color = "red",
                linewidth = 1.0
            )
    
    # Save map as PNG ...
    matplotlib.pyplot.savefig(
        "land_vs_latitude.png",
        bbox_inches = "tight",
        dpi = 300,
        pad_inches = 0.1
    )
    matplotlib.pyplot.close("all")
    pyguymer.optipng("land_vs_latitude.png")
    
    # Save data as CSV ...
    with open("land_vs_latitude.csv", "wt") as fobj:
        fobj.write("latitude [deg],length of land [deg]\n")
        for i in xrange(lats.size):
            fobj.write("{0:e},{1:e}\n".format(lats[i], lands[i]))
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

---
title: example background OS image raster (1)
date: 2020-05-07
---
Example Python program example-background-OS-image-raster (1).py

## Modules

* import json
* import os
* import cartopy
* import cartopy.crs
* import matplotlib
* import matplotlib.pyplot
* import pyguymer3

## Code

Python example

    #!/usr/bin/env python3
    
    # Import standard modules ...
    import json
    import os
    
    # Import special modules ...
    try:
        import cartopy
        import cartopy.crs
    except:
        raise Exception("run \"pip install --user cartopy\"")
    try:
        import matplotlib
        matplotlib.use("Agg")                                                       # NOTE: https://matplotlib.org/gallery/user_interfaces/canvasagg.html
        import matplotlib.pyplot
    except:
        raise Exception("run \"pip install --user matplotlib\"")
    
    # Import my modules ...
    try:
        import pyguymer3
    except:
        raise Exception("you need to have the Python module from https://github.com/Guymer/PyGuymer3 located somewhere in your $PYTHONPATH")
    
    # Set point and its bounding box ...
    point = (-1.463097, 52.915709)                                                  # [°], [°]
    xmin = point[0] - 0.3                                                           # [°]
    xmax = point[0] + 0.3                                                           # [°]
    ymin = point[1] - 0.3                                                           # [°]
    ymax = point[1] + 0.3                                                           # [°]
    
    # Set resolution and number of bearings ...
    dpi = 300                                                                       # [px/in]
    nang = 361
    
    # Create short-hand for the colour map ...
    cmap = matplotlib.pyplot.get_cmap("jet")
    
    # Define image root and load tile metadata ...
    root = "/path/to/ordnance/survey/background/images"
    meta = json.load(open(os.path.join(root, "raster.json"), "rt"))
    
    # ******************************************************************************
    
    # Create figure ...
    fg = matplotlib.pyplot.figure(figsize = (9, 6), dpi = dpi)
    ax = matplotlib.pyplot.axes(projection = cartopy.crs.PlateCarree())
    ax.set_extent([xmin, xmax, ymin, ymax])
    ax.set_title("Derby Train Station")
    
    # Initialize float and lists and draw data ...
    dist = 0.0                                                                      # [m]
    labels = []
    lines = []
    ax.scatter(
        [point[0]],
        [point[1]],
        alpha = 1.0,
        edgecolor = "none",
        facecolor = "red",
        transform = cartopy.crs.PlateCarree(),
    )
    for i in range(6):
        dist += 2500.0                                                              # [m]
        ax.add_geometries(
            [pyguymer3.buffer_point(point[0], point[1], dist, nang = nang)],
            cartopy.crs.PlateCarree(),
            alpha = 1.0,
            edgecolor = cmap(float(i) / 5.0),
            facecolor = "none",
            linewidth = 1.0
        )
        labels.append("{:.1f} km".format(0.001 * dist))
        lines.append(matplotlib.lines.Line2D([], [], color = cmap(float(i) / 5.0)))
    
    # Draw background image ...
    ax.imshow(
        matplotlib.pyplot.imread(os.path.join(root, meta["SK"]["greyscale"])),
        cmap = "gray",
        extent = meta["SK"]["extent"],
        interpolation = "bicubic",
        origin = "upper",
        transform = cartopy.crs.OSGB(),
        vmin = 0.0,
        vmax = 1.0
    )
    
    # Add legend and save figure ...
    ax.legend(lines, labels, bbox_to_anchor = (1.0, 0.5), fontsize = "small", ncol = 1)
    fg.savefig("raster.png", bbox_inches = "tight", dpi = dpi, pad_inches = 0.1)
    pyguymer3.exiftool("raster.png")
    pyguymer3.optipng("raster.png")
    matplotlib.pyplot.close("all")
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

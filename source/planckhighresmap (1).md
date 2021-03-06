---
title: planckhighresmap (1)
date: 2020-05-07
---
Example Python program planckhighresmap (1).py
For Python version 2.x.
To test your Python version use:

    python --version

## Modules

* import matplotlib
* import healpy as hp
* import matplotlib.pyplot as plt
* from matplotlib.colors import ListedColormap
* import numpy as np

## Code

Python example

    # Script by Andrea Zonca, http://zonca.github.io
    
    import matplotlib
    matplotlib.use("agg")
    import healpy as hp
    import matplotlib.pyplot as plt
    
    use_planck_cmap = True
    # Colormap available from https://github.com/zonca/paperplots/raw/master/data/Planck_Parchment_RGB.txt
    # Maps available at: http://irsa.ipac.caltech.edu/data/Planck/release_1/all-sky-maps/
    input_filename = "COM_CompMap_CMB-smica_2048_R1.20.fits"
    m=hp.read_map(input_filename, ("INP_CMB",))
    
    cmap = None
    out_filename = input_filename.split(".")[0]
    if use_planck_cmap:
        ############### CMB colormap
        from matplotlib.colors import ListedColormap
        import numpy as np
        colombi1_cmap = ListedColormap(np.loadtxt("Planck_Parchment_RGB.txt")/255.)
        colombi1_cmap.set_bad("gray") # color of missing pixels
        colombi1_cmap.set_under("white") # color of background, necessary if you want to use
        # this colormap directly with hp.mollview(m, cmap=colombi1_cmap)
        cmap = colombi1_cmap
        out_filename += "_planck_cmap"
    
    dpi = 300
    figsize_inch = 60, 40
    fig = plt.figure(figsize=figsize_inch, dpi=dpi)
    
    print "Mollview"
    # removed the colorbar, the map range is -500 / +500 microK
    hp.mollview(m, fig=fig.number, xsize=figsize_inch[0]*dpi, min=-500, max=500, title="", cbar=False, cmap=cmap)
    
    print "Save"
    plt.savefig(out_filename + ".png", dpi=dpi, bbox_inches="tight")

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

---
title: logo (1)
date: 2020-05-07
---
Example Python program logo (1).py

## Modules

* import cartopy.crs as ccrs
* import matplotlib.textpath
* import matplotlib.patches
* from matplotlib.font_manager import FontProperties
* import numpy as np

## Methods

* def main(ax):
* def on_draw(event=None):

## Code

Python example

    import cartopy.crs as ccrs
    import matplotlib.textpath
    import matplotlib.patches
    from matplotlib.font_manager import FontProperties
    import numpy as np
    
    
    def main(ax):
        # Comes from the cartopy gallery: http://scitools.org.uk/cartopy/docs/latest/examples/logo.html
    
        # generate a matplotlib path representing the word "cartopy"
        fp = FontProperties(family='Bitstream Vera Sans', weight='bold')
        logo_path = matplotlib.textpath.TextPath((-175, -35), 'cartopy',
                                                 size=80, prop=fp)
        # scale the letters up to sensible longitude and latitude sizes
        logo_path._vertices *= np.array([1, 2])
    
        im = ax.stock_img()
    
        def on_draw(event=None):
            """
            Hooks into matplotlib's event mechanism to define the clip path of the
            background image.
    
            """
            plate_carree_transform = ccrs.PlateCarree()._as_mpl_transform(ax)
            im.set_clip_path(logo_path, transform=plate_carree_transform)
    
        # Register the on_draw method and call it once now.
        ax.figure.canvas.mpl_connect('draw_event', on_draw)
        on_draw()
    
        # add the path as a patch, drawing black outlines around the text
        patch = matplotlib.patches.PathPatch(logo_path,
                                             antialiased=True,
                                             facecolor='none', edgecolor='black',
                                             transform=ccrs.PlateCarree())
        ax.add_patch(patch)
    
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

---
title: figure
date: 2020-05-07
---
Example Python program figure.py

## Modules

* import pyavm
* from wcsaxes import WCSAxes
* from matplotlib import pyplot as pl
* from matplotlib import pyplot as plt
* from PIL import Image
* import matplotlib
* from astropy import coordinates
* from astropy import units as u
* import numpy as np
* import pyregion
* import aplpy

## Methods

* def show_image(filename, rect=[0.075, 0.1, 0.8, 0.8], fig=None, xmpind=0):

## Code

Python example

    import pyavm
    from wcsaxes import WCSAxes
    from matplotlib import pyplot as pl
    from matplotlib import pyplot as plt
    from PIL import Image
    import matplotlib
    from astropy import coordinates
    from astropy import units as u
    import numpy as np
    import pyregion
    import aplpy
    
    def show_image(filename, rect=[0.075, 0.1, 0.8, 0.8], fig=None, xmpind=0):
        avm = pyavm.AVM.from_image(filename, xmp_packet_index=xmpind)
        wcs = avm.to_wcs(target_image=filename)
        if fig is None:
            fig = plt.gcf()
            
        ax = WCSAxes(fig, rect, wcs=wcs)
        fig.add_axes(ax)
    
        img = np.array(Image.open(filename).transpose(Image.FLIP_TOP_BOTTOM))
    
        ax.imshow(img, origin='lower')
    
        #ax.grid()
        
        return fig,ax
    
    fig = plt.figure(1, figsize=[14,14])
    fig.clf()
    fig,ax = show_image('eso1145a.tif',fig=fig,xmpind=1)
    
    regions = pyregion.open('supercam_targets.reg')
    
    
    for r in regions:
        x,y,w,h,a = r.coord_list
        rect = matplotlib.patches.Rectangle((x, y), w/np.abs(np.cos(y/180.*np.pi)),
                                            h, transform=ax.get_transform('fk5'),
                                            facecolor='none', edgecolor='w',
                                            linestyle='dotted')
        ax.add_patch(rect)
        
    pl.rcParams['font.size'] = 20
    ax.set_ylabel("Declination")
    ax.set_xlabel("Right Ascension")
    
    pl.savefig("CarinaLabocaPointings.jpg")
    
    fig2 = pl.figure(2)
    fig2.clf()
    F = aplpy.FITSFigure('eso1145a.tif',xmp_packet_index=1,figure=fig2)
    F.show_rgb()
    F.show_regions('supercam_targets.reg')
    F.tick_labels.set_xformat('hh:mm')
    F.tick_labels.set_yformat('dd:mm')
    F.save('CarinaLabocaPointings_aplpy.jpg')
    
    pl.show()
    #rects = matplotlib.collections.RegularPolygonCollection(numsides=4, sizes=
    #ax.add_
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

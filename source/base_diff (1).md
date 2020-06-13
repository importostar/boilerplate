---
title: base_diff (1)
date: 2020-05-07
---
Example Python program base_diff (1).py

## Modules

* from __future__ import division
* import numpy as np
* import sunpy.map as sm
* import matplotlib
* import matplotlib.pyplot as plt
* import matplotlib.colors as colors
* from matplotlib import patches
* from datetime import date, datetime, timedelta
* import astropy.units as u
* from sys import argv
* import sunpy.physics.differential_rotation as diffrot
* import matplotlib.colors as colors

## Code

Python example

    from __future__ import division
    import numpy as np
    import sunpy.map as sm
    import matplotlib
    import matplotlib.pyplot as plt
    import matplotlib.colors as colors
    from matplotlib import patches
    from datetime import date, datetime, timedelta
    import astropy.units as u
    from sys import argv
    import sunpy.physics.differential_rotation as diffrot
    import matplotlib.colors as colors
    
    script, aia1, aia2, mag = argv
    
    # Create the AIA maps and differentially rotate the first one
    a1map = sm.Map(aia1)
    a2map = sm.Map(aia2)
    a1map_rot= diffrot.diffrot_map(a1map, time=a2map.date)
    
    # Create base difference map
    diffdata=a2map.data-a1map_rot.data
    smap=sm.Map(np.clip(diffdata,-400,400),a2map.meta)
    smap.plot_settings['norm'] = colors.Normalize()
    
    # Create magnetogram map
    mmap = sm.Map(mag).rotate(order=3)
    mmap.plot_settings['cmap'] = plt.cm.bwr
    
    # Create composite map
    cmap = sm.Map(smap,mmap,composite=True)
    levels=[-200,200]
    cmap.set_levels(1,levels) #levels are contours
    
    # Make the plot
    fig = plt.figure()
    ax = plt.subplot(111)
    cmap.plot()
    plt.set_cmap('Greys_r')
    ax.xaxis.label.set_size(15)
    ax.yaxis.label.set_size(15)
    ax.tick_params(axis='both', which='major', labelsize=12)
    plt.xlim(-0.11,0)
    plt.ylim(-0.11,0)
    #plt.xlim(-400/3653,0)
    #plt.ylim(-400/3653,0)
    ax.set_xlabel('Solar-X [arcsec]')
    ax.set_ylabel('Solar-Y [arcsec]')
    plt.title('')
    #plt.axis('off')
    #ax.xaxis.set_visible(False)
    #ax.yaxis.set_visible(False)
    
    #ax.text(0.98, 0.01, '{:%Y-%m-%d %H:%M} - 22:00'.format(a2map.date), #0.62 first, 0.52 after 
    #        verticalalignment='bottom', horizontalalignment='right',
    #        transform=ax.transAxes, zorder=0,
    #        color='black', fontsize=18)
    
    #fig.savefig('diff1.png', dpi=200, bbox_inches='tight')
    #fig.savefig('diff1.eps', format='eps', bbox_inches='tight', pad_inches=0.01)
    
    plt.show()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

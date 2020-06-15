---
title: example_great_ani
date: 2020-05-07
---
Example Python program example_great_ani.py

## Modules

* import matplotlib
* from mpl_toolkits.basemap import Basemap
* import matplotlib.pyplot as plt
* import matplotlib.animation as ani
* import numpy as np

## Code

Python example

    import matplotlib
    matplotlib.use("Agg")
    
    from mpl_toolkits.basemap import Basemap
    import matplotlib.pyplot as plt
    import matplotlib.animation as ani
    import numpy as np
    
    fig = plt.figure(figsize=(12, 7))
    
    nylat = 40.730610
    nylon = -73.935242
    sflat = 37.773972
    sflon = -122.431297
    drw_lst = []
    
    
    FFMpegWriter = ani.writers['ffmpeg']
    metadata = dict(title='Ani DGC Example', artist='Matplotlib',
                    comment='Movie support!')
    writer = FFMpegWriter(fps=3, metadata=metadata)
    
    
    ax = fig.add_subplot(221)
    ax.set_title('Regular DGC')
    m = Basemap(llcrnrlon=-119, llcrnrlat=22, urcrnrlon=-54, urcrnrlat=55, projection='lcc', resolution='l', lat_1=32,
                lat_2=45, lon_0=-95)
    m.drawcoastlines()
    
    # Grab points along line for animating.
    dgc = m.drawgreatcircle(nylon, nylat, sflon ,sflat, linewidth=2, color='b', del_s=50)
    dgc_path = [d for d in dgc.iter_segments()]
    
    for a, b in dgc_path:
        q, r = tuple(a)
        drw_lst += [[q] + [r]]
    
    with writer.saving(fig, 'Ani_DGC_Example.mp4', 300):
    
        for a, b in drw_lst:
    
            ax = fig.add_subplot(222)
            ax.set_title('Animated DGC')
            m = Basemap(llcrnrlon=-119, llcrnrlat=22, urcrnrlon=-54, urcrnrlat=55, projection='lcc', resolution='l',
                        lat_1=32, lat_2=45, lon_0=-95)
            m.drawcoastlines()
            ax.plot(a, b, marker='.', color='b', markersize=6)
    
            ax = fig.add_subplot(223)
            ax.set_title('Animated DGC w/ random color')
            m = Basemap(llcrnrlon=-119, llcrnrlat=22, urcrnrlon=-54, urcrnrlat=55, projection='lcc', resolution='l',
                        lat_1=32, lat_2=45, lon_0=-95)
            m.drawcoastlines()
            ax.plot(a, b, marker='.', color=np.random.rand(3,1), markersize=6)
    
            ax = fig.add_subplot(224)
            ax.set_title('Animated DGC single dot')
            m = Basemap(llcrnrlon=-119, llcrnrlat=22, urcrnrlon=-54, urcrnrlat=55, projection='lcc', resolution='l',
                        lat_1=32, lat_2=45, lon_0=-95)
            m.drawcoastlines()
            pta = ax.plot(a, b, marker='.', color='b', markersize=8)
            writer.grab_frame()
            cp = pta.pop(0)
            cp.remove()
            del cp
    
        writer.grab_frame()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

---
title: rand_hop_paths_movie
date: 2020-05-07
---
Example Python program rand_hop_paths_movie.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import pygeoip
* import matplotlib
* import matplotlib.pyplot as plt
* import matplotlib as mpl
* import matplotlib.animation as manimation
* import random
* import numpy as np
* from mpl_toolkits.basemap import Basemap
* from collections import OrderedDict
* from geopy.geocoders import Nominatim

## Methods

* def ran_colors():
* def drawdimcircles(lat, lon, lat2, lon2, color):

## Code

Python example

    '''
    Need GeoLiteCity.dat
    https://dev.maxmind.com/geoip/legacy/geolite/
    
    Need FFMEPG
    https://ffmpeg.zeranoe.com/builds/
    
    Both in root of rand_hop_paths_movie.py
    '''
    
    
    import pygeoip
    import matplotlib
    matplotlib.use("Agg")
    import matplotlib.pyplot as plt
    import matplotlib as mpl
    import matplotlib.animation as manimation
    import random
    import numpy as np
    
    from mpl_toolkits.basemap import Basemap
    from collections import OrderedDict
    from geopy.geocoders import Nominatim
    geolocator = Nominatim()
    #Edit here
    #how many random Class C IP addresses you want to run?
    c = 10
    #
    
    colors = ['b', 'g', 'r', 'c', 'm', 'y', 'k', 'w']
    
    #Map settings
    fig = plt.figure(figsize=(16, 9), dpi=100, frameon=False, tight_layout=True)
    ax = plt.subplot(111)
    plt.subplots_adjust(left=0.05,right=0.95,top=0.90,bottom=0.05,wspace=0.15,hspace=0.05)
    
    m = Basemap(projection='robin', lat_0=0, lon_0=-100, resolution='l', area_thresh=100000.0)
    m.drawmapboundary(fill_color='#1F1F1F')
    m.drawcoastlines()
    m.drawstates()
    m.drawcountries()
    m.fillcontinents(color='#3C3C3C', lake_color='#1F1F1F')
    m.drawmeridians(np.arange(0, 360, 30))
    m.drawparallels(np.arange(-90, 90, 30))
    title_string = str(c) + ' Random IP Connections'
    plt.title(title_string)
    filename = title_string + '.mp4'
    
    cord_lst = []
    gclines = []
    color_lst = []
    
    FFMpegWriter = manimation.writers['ffmpeg']
    metadata = dict(title=title_string, artist='Me',
                    comment='Movie!')
    writer = FFMpegWriter(fps=3, metadata=metadata)
    
    def ran_colors():
        ran_color = random.randint(0, 7)
        return colors[ran_color]
    
    while c > 0:
        ##Class C range - 128.0.0.0 191.255.255.255
        oct1_r = random.randint(128, 191)
        oct_r = random.randint(0, 255)
    
        IP = str(oct1_r) + '.' + str(oct_r) + '.' + str(oct_r) + '.' + str(oct_r)
    
        try:
            color = ran_colors()
            gi = pygeoip.GeoIP('GeoLiteCity.dat')
            gir = gi.record_by_addr(IP)
            if not isinstance(gir['city'], unicode):
                pass
            else:
                cord_lst += [[str(gir['latitude'])] + [str(gir['longitude'])] + [str(gir['city'])] + [IP] + [color]]
                c -= 1
        except Exception:
            pass
    
    for (lat, lon, city, ip, color) in cord_lst:
        gclines += [lon] + [lat]
        color_lst += [color]
    
    def drawdimcircles(lat, lon, lat2, lon2, color):
        val_lst = []
        poop = m.drawgreatcircle(lat, lon, lat2, lon2, linewidth=2, alpha=0, color=color, del_s=100)
        path = poop.iter_segments()
        for val in path:
            val_lst += [val]
    
        for x, y in val_lst:
            q, r = tuple(x)
            ax.plot(q, r, marker='.', color=color, markersize=6, alpha=.5)
            writer.grab_frame()
        writer.grab_frame()
        print('line') #just to make sure it's running
    
    with writer.saving(fig, filename, 300):
    
        for i, j, k, l, z in zip(gclines[0::2], gclines[1::2], gclines[2::2], gclines[3::2], color_lst):
            x, y = m(i, j)
            ax.plot(x, y, marker='.', color=z, markersize=50, alpha=0.09)
            writer.grab_frame()
            drawdimcircles(float(i), float(j), float(k), float(l), z)
    
        writer.grab_frame()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

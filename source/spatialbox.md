---
title: spatialbox
date: 2020-05-07
---
Example Python program spatialbox.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import sys
* from geopy.geocoders import GoogleV3
* from matplotlib import pyplot
* from shapely.geometry import LineString
* from descartes import PolygonPatch
* import cartopy
* import matplotlib.pyplot as plt
* from mpl_toolkits.basemap import Basemap
* import numpy as np
* import matplotlib.pyplot as plt
* import fiona
* import pysal
* from pyproj import Proj, transform
* import geopandas as gpd
* from bokeh.plotting import figure
* from bokeh.io import output_notebook, show
* from bokeh.models import GeoJSONDataSource
* import geopandas as gpd
* from bokeh.resources import INLINE
* import seaborn as sns
* from shapely.geometry import *
* import matplotlib.pyplot as plt
* import geopandas as gpd
* import folium

## Methods

* def plot_line(ax, ob):

## Code

Python example

    # coding: utf-8
    
    # In[37]:
    
    import sys
    print sys.version
    
    
    # ## Geopy
    
    # In[38]:
    
    from geopy.geocoders import GoogleV3
    
    addresses = ['Liverpool Rd, Manchester M3 4FP, United Kingdom',
                 'Albert Square, Manchester M60 2LA, United Kingdom',
                 'St Anns Square, Manchester M2 7DH, United Kingdom']
    
    gc = GoogleV3()
    
    points = []
    for address in addresses:
        loc = gc.geocode(address)
        print loc.address, (loc.latitude, loc.longitude)
    
    
    # ## Descartes & Shapely
    
    # In[39]:
    
    get_ipython().magic(u'matplotlib inline')
    from matplotlib import pyplot
    from shapely.geometry import LineString
    from descartes import PolygonPatch
    
    BLUE = '#6699cc'
    GRAY = '#999999'
    
    def plot_line(ax, ob):
        x, y = ob.xy
        ax.plot(x, y, color=GRAY, linewidth=3, solid_capstyle='round', zorder=1)
    
    line = LineString([(0, 0), (1, 1), (0, 2), (2, 2), (3, 1), (1, 0)])
    
    fig = pyplot.figure(1, figsize=(10, 4), dpi=180)
    ax = fig.add_subplot(121)
    plot_line(ax, line)
    
    
    # ## Cartopy
    
    # In[40]:
    
    get_ipython().magic(u'matplotlib inline')
    import cartopy
    import matplotlib.pyplot as plt
    
    ax = plt.axes(projection=cartopy.crs.PlateCarree())
    
    ax.add_feature(cartopy.feature.LAND)
    ax.add_feature(cartopy.feature.OCEAN)
    ax.add_feature(cartopy.feature.COASTLINE)
    ax.add_feature(cartopy.feature.BORDERS, linestyle=':')
    ax.add_feature(cartopy.feature.LAKES, alpha=0.5)
    ax.add_feature(cartopy.feature.RIVERS)
    ax.set_extent([-20, 60, -40, 40])
    
    ax.set_title('Africa')
    
    plt.show()
    
    
    # ## Matplotlib Basemap
    
    # In[41]:
    
    get_ipython().magic(u'matplotlib inline')
    from mpl_toolkits.basemap import Basemap
    import numpy as np
    import matplotlib.pyplot as plt
    width = 28000000
    lon_0 = 60
    lat_0 = 45
    m = Basemap(width=width,height=width,projection='aeqd',
                lat_0=lat_0,lon_0=lon_0,llcrnrlon=0,urcrnrlon=90, llcrnrlat=0,urcrnrlat=70)
    # fill background.
    m.drawmapboundary(fill_color='aqua')
    # draw coasts and fill continents.
    m.drawcoastlines(linewidth=0.5)
    m.fillcontinents(color='coral',lake_color='aqua')
    # 20 degree graticule.
    m.drawparallels(np.arange(-80,81,20))
    m.drawmeridians(np.arange(-180,180,20))
    # draw a black dot at the center.
    xpt, ypt = m(lon_0, lat_0)
    # draw the title.
    plt.title('Azimuthal Equidistant Projection')
    
    m.plot([xpt],[ypt],'ko')
    
    
    # ## Fiona
    
    # In[42]:
    
    import fiona
    c = fiona.open(r'C:\Program Files (x86)\ArcGIS\Desktop10.4\ArcGlobeData\continent.shp', 'r')
    len(list(c))
    
    
    # ## Pysal
    
    # In[43]:
    
    import pysal
    shp = pysal.open(r'C:\Program Files (x86)\ArcGIS\Desktop10.4\ArcGlobeData\continent.shp')
    poly = shp.next()
    print type(poly)
    print len(shp)
    print poly.centroid
    print poly.area
    
    
    # ## Pyproj
    
    # In[44]:
    
    from pyproj import Proj, transform
    
    inProj = Proj(init='epsg:3857')
    outProj = Proj(init='epsg:4326')
    x1,y1 = -11705274.6374,4826473.6922
    x2,y2 = transform(inProj,outProj,x1,y1)
    print x2,y2
    
    
    # ## Geopandas
    
    # In[45]:
    
    import geopandas as gpd
    gdf = gpd.read_file(r'C:\Program Files (x86)\ArcGIS\Desktop10.4\ArcGlobeData\continent.shp')
    gdf['Area'] = gdf.area
    
    
    # In[46]:
    
    gdf.plot(figsize=(20,20),column='Area',cmap='OrRd')
    
    
    # ## Bokeh
    
    # In[47]:
    
    from bokeh.plotting import figure
    from bokeh.io import output_notebook, show
    from bokeh.models import GeoJSONDataSource
    import geopandas as gpd
    
    
    # In[48]:
    
    output_notebook()
    
    
    # In[49]:
    
    from bokeh.resources import INLINE
    output_notebook(resources=INLINE)
    
    
    # In[50]:
    
    gdf = gpd.read_file(r'C:\Program Files (x86)\ArcGIS\Desktop10.4\TemplateData\TemplateData.gdb',
                        layer='counties')
    
    gdf = gdf[gdf.STATE_NAME == 'Texas']
    gdf_series = gdf['geometry']
    
    all_coords_x = []
    all_coords_y = []
    
    for i in gdf_series:
        for l in i.boundary:        
            all_coords_x.append(list(l.coords.xy[0]))
            all_coords_y.append(list(l.coords.xy[1]))
    
    p = figure(plot_width=600, plot_height=600)
    p.patches(xs=all_coords_x,ys=all_coords_y,
              color="green", alpha=0.6, line_width=1)
    show(p)
    
    
    # ## Seaborn
    
    # In[51]:
    
    import seaborn as sns
    from shapely.geometry import *
    import matplotlib.pyplot as plt
    
    pnts = [{3134: [-158.06185681320747, 21.493171207639477]},
    {3143: [-157.91885505740734, 21.376283075276433]},
    {3144: [-157.80145638193602, 21.314083401697474]},
    {3150: [-155.5, 20.25]},
    {3151: [-155.8, 20.45]},
    {3145: [-158.0090502554755, 21.31298880746067]},
    {3149: [-155.08472452266503, 19.693112205773275]}]
    
    points = [Point(list(i.values())[0][0],list(i.values())[0][1]) for i in pnts]
    
    poly_coords = [(-156,20), (-156,21), (-155,21), (-155,20),(-156,20)]
    poly = Polygon(poly_coords)
    
    poly_xs = [i for i,j in poly_coords]
    poly_ys = [j for i,j in poly_coords]
    
    pnt_xs = [p.x for p in points]
    pnt_ys = [p.y for p in points]
    
    fig = plt.figure()
    axes = fig.gca()
    axes.set_xlim([-159,-154])
    axes.set_ylim([19,22])
    
    axes.plot(poly_xs,poly_ys)
    axes.plot(pnt_xs,pnt_ys,'ro')
    
    intersected_pnts = [p for p in points if poly.intersects(p)]
    print(intersected_pnts)
    
    plt.show()
    
    
    # ## Folium
    
    # In[52]:
    
    import geopandas as gpd
    import folium
    
    datasrc_path = r'C:\Program Files (x86)\ArcGIS\Desktop10.4\TemplateData\TemplateData.gdb'
    lakes = gpd.read_file(datasrc_path,layer='us_lakes')
    
    m = folium.Map([40.7,-90], zoom_start=4, tiles='cartodbpositron')
    folium.GeoJson(lakes).add_to(m)
    
    m

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

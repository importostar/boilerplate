---
title: Tectonique
date: 2020-05-07
---
Example Python program Tectonique.py

## Modules

* import matplotlib # no UI backend
* import pandas as pd
* import numpy as np
* from mpl_toolkits.basemap import Basemap
* import matplotlib.pyplot as plt
* from sqlite3 import *
* from koala import Koala

## Code

Python example

    import matplotlib # no UI backend
    matplotlib.use('Agg') # no UI backend
    
    import pandas as pd
    import numpy as np
    
    from mpl_toolkits.basemap import Basemap
    
    import matplotlib.pyplot as plt
    
    from sqlite3 import *
    
    from koala import Koala
    
    
    
    
    # Récuperation de la base de données GPS
    
    con = connect("gps.db")
    
    brazz = pd.read_sql_query("select * from brazz", con)
    eisl = pd.read_sql_query("select * from eisl", con)
    pama = pd.read_sql_query("select * from pama", con)
    
    
    # Mesure des déplacements lat et long des 3 stations gps
    
    kbrazz = Koala(brazz)
    
    lat_brazz = kbrazz.lin("temps", "lat")
    lon_brazz = kbrazz.lin("temps", "long")
    
    v_lat_brazz = lat_brazz.a
    v_lon_brazz = lon_brazz.a
    n_brazz = round((v_lon_brazz**2 + v_lat_brazz**2)**0.5,2)
    
    keisl = Koala(eisl)
    
    lat_eisl = keisl.lin("temps", "lat")
    lon_eisl = keisl.lin("temps", "long")
    
    v_lat_eisl = lat_eisl.a
    v_lon_eisl = lon_eisl.a
    n_eisl = round((v_lon_eisl**2 + v_lat_eisl**2)**0.5,2)
    
    kpama = Koala(pama)
    
    lat_pama = kpama.lin("temps", "lat")
    lon_pama = kpama.lin("temps", "long")
    
    v_lat_pama = lat_pama.a
    v_lon_pama = lon_pama.a
    n_pama = round((v_lon_pama**2 + v_lat_pama**2)**0.5,2)
    
    vecteur = {"brazz":(v_lon_brazz, v_lat_brazz, n_brazz), "eisl":(v_lon_eisl, v_lat_eisl, n_eisl), "pama":(v_lon_pama, v_lat_pama, n_pama)}
    
    
    plt.close()
    
    
    # Création du fond de carte
    
    map = Basemap(projection='aeqd', lon_0 = -85, lat_0 = 10, width = 18000000, height = 15000000)
    
    map.etopo()
    
    map.drawcoastlines()
    
    map.drawmeridians(range(0,360,60), dashes=[3,1], linewidth=0.5, labels=[0,0,0,1], zorder=2)
    map.drawparallels(range(-40,50,10), dashes=[4,2], linewidth=0.5, labels=[1,0,0,0], zorder=1)
    
    plt.savefig("font.png")
    
    
    
    # Placement des foyers sismiques
    
    seismes = pd.read_csv("earthquakes.csv") # https://gist.github.com/astrofrog/b29141f2b39bb2dfe7ce
    
    df = seismes.loc[:,["latitude", "longitude"]]
    
    for i in range(len(df)):
        
        x, y = df.longitude[i], df.latitude[i]
    
        try:
            x, y = map(x,y)
    
            map.plot(x, y, marker='*', color='y', markersize=2)
    
        except:
    
            pass
    
    plt.savefig("seismes.png")
    
    
    
    # Placement des volcans actifs depuis 1900
    
    volcans = pd.read_excel("https://query.data.world/s/jejujyib5byfslvmbixubz6leb3f4d")
    
    vf = volcans.loc[:,["Year", "Latitude", "Longitude"]]
    
    for v in range(len(vf)):
    
        if vf.Year[v] > 1900:
    
            x, y = vf.Longitude[v], vf.Latitude[v]
    
            try:
    
                x, y = map(x,y)
    
                map.plot(x, y, marker='*', color="r", markersize=2)
    
            except:
    
                pass
    
    plt.savefig("vulcan.png")
    
    
    
    
    # Placement des stations GPS
    
    stations = [("EISL", -109.57, -27.14), ("PAMA", -149.57, -17.56), ("BRAZZ", -47.80, -15.90)] # liste de tuple (nom, lon, lat)
    
    for s in stations:
        
        x, y = map(s[1], s[2])
        
        map.plot(x, y, marker='+', markersize=10, color="k")
        
        plt.text(x, y, s[0], ha = "left", va = "top", fontsize =8)
    
    plt.savefig("gpscarte.png")
    
    
    
    
    # Placement des vecteurs déplacements sur la carte
    
    x, y = map(stations[0][1], stations[0][2])
    
    map.quiver(x, y, v_lon_eisl, v_lat_eisl, scale_units='inches', scale=8, headwidth=12, headlength=15, units='inches', width=0.01)
    
    x, y = map(stations[1][1], stations[1][2])
    
    map.quiver(x, y, v_lon_pama, v_lat_pama, scale_units='inches', scale=14, headwidth=12, headlength=15, units='inches', width=0.01)
    
    x, y = map(stations[2][1], stations[2][2])
    
    map.quiver(x, y, v_lon_brazz, v_lat_brazz, scale_units='inches', scale=8, headwidth=12, headlength=10, units="inches", width=0.01)
    
    for s in stations:
    	
        x, y = map(s[1], s[2])
        
        plt.text(x, y," v =  " + str( vecteur[str.lower(s[0])][2]) + " cm/an", ha="left", va="bottom", fontsize=6)
    
    plt.savefig("vecteur.png")

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

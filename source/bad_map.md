---
title: bad_map
date: 2020-05-07
---
Example Python program bad_map.py

## Modules

* import shapefile
* import matplotlib.cm as jimbo
* import matplotlib.pyplot as plt
* import matplotlib.patches as patches
* from matplotlib.patches import Polygon
* from matplotlib.collections import PatchCollection
* import numpy as np

## Code

Python example

    """ I did not write this, though I fixed a syntax error in it. I just found it while looking for an easy way to plot a world choropleth map. It is probably the worst program I've ever seen and felt I should keep it for some reason. """ 
    
    import shapefile
    import matplotlib.cm as jimbo
    import matplotlib.pyplot as plt
    import matplotlib.patches as patches
    from matplotlib.patches import Polygon
    from matplotlib.collections import PatchCollection
    import numpy as np
    
    #   -- input --
    sf = shapefile.Reader("ne_110m_admin_0_countries.shp")
    recs    = sf.records()
    shapes  = sf.shapes()
    Nshp    = len(shapes)
    cns     = []
    for nshp in xrange(Nshp):
        cns.append(recs[nshp][1])
    cns = np.array(cns)
    cm    = jimbo.get_cmap('Dark2')
    cccol = cm(1.*np.arange(Nshp)/Nshp)
    #   -- plot --
    fig     = plt.figure()
    ax      = fig.add_subplot(111)
    for nshp in xrange(Nshp):
        ptchs   = []
        pts     = np.array(shapes[nshp].points)
        prt     = shapes[nshp].parts
        par     = list(prt) + [pts.shape[0]]
        for pij in xrange(len(prt)):
         ptchs.append(Polygon(pts[par[pij]:par[pij+1]]))
        ax.add_collection(PatchCollection(ptchs,facecolor=cccol[nshp,:],edgecolor='k', linewidths=.1))
    ax.set_xlim(-180,+180)
    ax.set_ylim(-90,90)
    
    #fig.savefig('test.png')
    plt.show()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

---
title: beachball
date: 2020-05-07
---
Example Python program beachball.py

## Modules

* from __future__ import (absolute_import, division, print_function,
* import matplotlib.pyplot as plt
* import matplotlib.collections as mcollections
* import matplotlib.patches as mpatches
* import matplotlib.transforms as mtransforms

## Methods

* def beach(axes):

## Code

Python example

    # -*- coding: utf-8 -*-
    from __future__ import (absolute_import, division, print_function,
                            unicode_literals)
    
    import matplotlib.pyplot as plt
    import matplotlib.collections as mcollections
    import matplotlib.patches as mpatches
    import matplotlib.transforms as mtransforms
    
    
    def beach(axes):
        xy = (0, 0)
        paths = [
            mpatches.Ellipse(xy, width=400, height=400),
            mpatches.Ellipse(xy, width=300, height=300),
            mpatches.Ellipse(xy, width=200, height=200),
        ]
        colors = ['b', 'w', 'g']
    
        col = mcollections.PatchCollection(paths, match_original=False)
        col.set_facecolors(colors)
    
        # Use the given axes to maintain the aspect ratio of beachballs on figure
        # resize.
        # This is what holds the aspect ratio (but breaks the positioning)
        col.set_transform(mtransforms.IdentityTransform())
        # Next is a dirty hack to fix the positioning:
        # 1. Need to bring the all patches to the origin (0, 0).
        for p in col._paths:
            p.vertices -= xy
        # 2. Then use the offset property of the collection to position the
        #    patches
        col.set_offsets(xy)
        col._transOffset = axes.transData
    
        col.set_edgecolor('k')
    
        return col
    
    
    fig = plt.figure()
    ax = fig.add_subplot(111)
    ax.add_collection(beach(axes=ax))
    ax.axis([-10000, 10000, -100, 100])
    fig.savefig('bb_aspect_x.png')

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

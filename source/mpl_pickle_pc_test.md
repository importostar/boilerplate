---
title: mpl_pickle_pc_test
date: 2020-05-07
---
Example Python program mpl_pickle_pc_test.py

## Modules

* import matplotlib
* import cPickle as pickle
* import numpy as np
* import matplotlib.pyplot as plt
* from matplotlib.patches import Rectangle
* from matplotlib.collections import PatchCollection

## Code

Python example

    use_try = False # use try-except to ignore AttributeError
    
    import matplotlib
    matplotlib.rcdefaults()
    
    import cPickle as pickle
    import numpy as np
    import matplotlib.pyplot as plt
    
    from matplotlib.patches import Rectangle
    from matplotlib.collections import PatchCollection
    
    ## set up plot of four rectangles around the origin
    values = np.array([1, 2, 3, 4])
    cmap = 'gist_rainbow'
    
    x, y = ([-1, -1, 0, 0], [-1, 0, -1, 0])
    dx, dy = (1, 1)
    
    patches = [Rectangle(xy, width=dx, height=dy) for xy in zip(x, y)]
    pc = PatchCollection(patches)
    
    ## dump pickle before setting any attributes on the PatchCollection
    pickle.dump(pc, open('patch_collection_temp.pickle', 'w'))
    
    # set attributes
    pc.set_array(values)
    pc.set_cmap(cmap)
    
    # plot
    fig, ax = plt.subplots()
    ax.add_collection(pc)
    ax.axis([-1, 1, -1, 1])
    fig.savefig('pre_pickle_mpl_%s.png' % (matplotlib.__version__))
    plt.clf()
    
    ## load the pickled PatchCollection
    pc_loaded = pickle.load(open('patch_collection_temp.pickle'))
    
    # set attributes
    pc_loaded.set_array(values)
    if use_try:
        try:
            pc_loaded.set_cmap(cmap)
        except AttributeError:
            pass
    else:
        pc_loaded.set_cmap(cmap)
    
    # plot
    fig, ax = plt.subplots()
    ax.add_collection(pc_loaded)
    ax.axis([-1, 1, -1, 1])
    fig.savefig('post_pickle_mpl_%s.png' % (matplotlib.__version__))
    plt.clf()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

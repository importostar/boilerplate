---
title: categorical_vis
date: 2020-05-07
---
Example Python program categorical_vis.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* %pylab inline --no-import-all
* # import numpy as np
* # import matplotlib.pyplot as plt
* # import pylab
* import collections
* from pprint import pformat

## Methods

* def generate_data(constraints):
* def _standardize_constraints(constraints):
* def fits_constraints(data, constraints):
* def generate_data(constraints):
* def iter_adjacencies(data):
* def build_array_from_adj_list(data, adj_list):
* def draw_co_ocurrence_diagram(adj, categories, figsize=(4,5)):

## Code

Python example

    # -*- coding: utf-8 -*-
    # <nbformat>3.0</nbformat>
    
    # <markdowncell>
    
    # Draw a co-ocurrence matrix with matplotlib.matshow (matplotlib.imshow)
    # 
    # https://en.wikipedia.org/wiki/Co-occurrence_matrix
    # 
    # * https://en.wikipedia.org/wiki/Matplotlib
    # * http://matplotlib.org/api/pyplot_api.html#matplotlib.pyplot.matshow
    # * http://matplotlib.org/api/pyplot_api.html#matplotlib.pyplot.imshow
    # 
    # Created with IPython notebook in an Anaconda 1.9.1 environment
    # 
    # * http://ipython.org/notebook.html
    # * http://docs.continuum.io/anaconda/install.html
    # * http://docs.continuum.io/anaconda/pkgs.html
    
    # <codecell>
    
    %pylab inline --no-import-all
    # import numpy as np
    # import matplotlib.pyplot as plt
    # import pylab
    import collections
    from pprint import pformat
    
    # <codecell>
    
    DATA_CONSTRAINTS = (
        (('english',), 5),
        (('math',), 7),
        (('social studies',), 3),
        (('science',), 3),
        (('english', 'science'), 1),
        (('english', 'social studies',), 1),
        (('math', 'science'), 2),
        (('science', 'social studies',), 1)
    )
    
    def generate_data(constraints):
        """
        Args:
            constraints: ((categories_tuple,), count_int)
    
        Returns:
            list of category tuples satisfying constraints
    
        """
        def _standardize_constraints(constraints):
            return [(tuple(sorted(c[0])), c[1]) for c in constraints]
    
        def fits_constraints(data, constraints):
            dataset = list(data)
            counts = collections.Counter(tuple(sorted(elem)) for elem in dataset)
            _constraints = _standardize_constraints(constraints)
            return sorted(counts.iteritems()) == sorted(_constraints)
    
        def generate_data(constraints):
            _constraints = _standardize_constraints(constraints)
            for categories, count in _constraints:
                for n in xrange(count):
                    yield categories
    
        data = list(generate_data(constraints))
        if fits_constraints(data, constraints):
            return data
        raise Exception("uh") # XXX
    data = generate_data(DATA_CONSTRAINTS)
    data
    
    # <codecell>
    
    def iter_adjacencies(data):
        """
        Args:
            data: iterable of categories
        Returns:
            iterable of (row, (category_x, category_y)) pairs with self edges
        """
        for row_n, row in enumerate(data):
            _len = len(row)
            for category in row:
                yield (row_n,row), (category, category)
            if _len > 1:
                for i in xrange(_len-1):
                    yield (row_n,row), (row[i], row[i+1])
    
    adj_list = list(iter_adjacencies(data))
    adj_list
    
    # <codecell>
    
    def build_array_from_adj_list(data, adj_list):
        print(pformat(collections.Counter(data).items()))
        
        categories = collections.OrderedDict(
            (v,k) for k,v in enumerate(sorted(set(item for row in data for item in row))))
        print("Indices: %s" % categories)
        
        adjacency_dimensions = len(categories), len(categories)
        print(adjacency_dimensions)
        
        adj = np.zeros(adjacency_dimensions)
        #print(adj)
        
        for row, adjacencies in adj_list:
            x, y = categories.get(adjacencies[0]), categories.get(adjacencies[1])
            adj[x][y] += 1
            if x != y:
                adj[y][x] += 1
        print(adj)
        
        subtotal_0 = np.sum(adj, axis=0)
        subtotal_1 = np.sum(adj, axis=1)
        if not np.all(np.equal(subtotal_0, subtotal_1)):
            raise Exception("Should be the same")
        
        totals =  zip(categories.keys(), subtotal_0)
        print("Totals: %s" % totals)
        return adj, categories
    
    adj, categories = build_array_from_adj_list(data, adj_list)
    
    # <codecell>
    
    def draw_co_ocurrence_diagram(adj, categories, figsize=(4,5)):
        pylab.rcParams['figure.figsize'] = figsize
        plt.matshow(adj, cmap="Greys")
        ticks = (np.arange(len(categories)), categories.keys())
        plt.xticks(*ticks, rotation=90)
        plt.yticks(*ticks)
        plt.colorbar(orientation='horizontal')
    
    draw_co_ocurrence_diagram(adj, categories)
    
    # <codecell>
    
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

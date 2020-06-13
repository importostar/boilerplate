---
title: molahisto
date: 2020-05-07
---
Example Python program molahisto.py
For Python version 2.x.
To test your Python version use:

    python --version

## Modules

* from __future__ import unicode_literals
* import sys
* import numpy as np
* import matplotlib.mlab as mlab
* import matplotlib.pyplot as plt

## Code

Python example

    #!/usr/bin/env python
    # -*- coding: utf-8 -*-
    from __future__ import unicode_literals
    
    import sys
    import numpy as np
    import matplotlib.mlab as mlab
    import matplotlib.pyplot as plt
    
    width = 20  # cm
    height = 15 # cm
    
    if len(sys.argv) < 4:
      print "Usage: molahisto.py data.txt title output"
      exit(1)
    
    type = sys.argv[2].decode(encoding='UTF-8',errors='strict')
    output = sys.argv[3]
    
    data = np.fromfile(sys.argv[1], sep='\n')
    
    num_bins = 8
    
    fig, ax = plt.subplots()
    n, bins, patches = ax.hist(data, num_bins, color='burlywood', histtype='stepfilled')
    
    ax.set_xlabel('Constante Elástica (N/m)')
    ax.set_ylabel('Contagem')
    ax.set_title('%s' %type)
    ax.set_ylim( None, n.max() * 1.2)
    
    fig.tight_layout()
    
    fig.set_size_inches(width / 2.54, height / 2.54)
    plt.savefig('%s.png' %output, dpi=100)

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

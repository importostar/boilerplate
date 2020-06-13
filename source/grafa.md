---
title: grafa
date: 2020-05-07
---
Example Python program grafa.py
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
    
    deltaS = 34 # metros
    
    
    if len(sys.argv) < 4:
      print "Usage: generate.py data.txt type output"
      exit(1)
    
    type = sys.argv[2].decode(encoding='UTF-8',errors='strict')
    output = sys.argv[3]
    
    data = np.fromfile(sys.argv[1], sep='\n')
    
    data = (2 * 34) / (data ** 2)
    
    num_bins = 12
    avg = np.average(data)
    std = np.std(data)
    
    fig, ax = plt.subplots()
    n, bins, patches = ax.hist(data, num_bins, color='burlywood', histtype='stepfilled')
    
    print "Média: %s Desvio Padrão: %s" %(avg, std)
    
    ax.axvline(avg, color='red', label="Média = %.2f m/s²" %avg)
    ax.axvline(avg-std, color='lightblue', label="Média - Desvio Padrão = %.2f m/s²" %(avg-std))
    ax.axvline(avg+std, color='darkblue', label="Média + Desvio Padrão = %.2f m/s²" % (avg+std))
    
    ax.set_xlabel('Aceleração (m/s²)')
    ax.set_ylabel('Contagem (n)')
    ax.set_title('Histograma das Acelerações Médias (%s)' %type)
    ax.set_ylim( None, n.max() * 1.2)
    
    legend = ax.legend(loc='upper left', shadow=True, prop={'size':10})
    fig.tight_layout()
    
    fig.set_size_inches(width / 2.54, height / 2.54)
    plt.savefig('%s.png' %output, dpi=100)

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

---
title: hacky_rgyr_and_rdist
date: 2020-05-07
---
Example Python program hacky_rgyr_and_rdist.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import argparse
* import csv
* import sys
* import itertools
* import MDAnalysis as mda
* import matplotlib
* import matplotlib.pyplot as plt
* import numpy as np
* import numpy.linalg
* from MDAnalysis.analysis.dihedrals import Ramachandran
* import MDAnalysis as mda
* from MDAnalysis.lib.distances import calc_dihedrals
* import numpy.linalg
* import numpy as np
* import seaborn as sns
* from collections import namedtuple
* import numpy.linalg
* import seaborn as sns, numpy as np

## Code

Python example

    #!/usr/bin/env python
    # coding: utf-8
    
    # In[1]:
    
    
    import argparse
    import csv
    import sys
    
    import itertools
    import MDAnalysis as mda
    
    import matplotlib
    matplotlib.use('Agg')  # noqa
    get_ipython().run_line_magic('matplotlib', 'inline')
    import matplotlib.pyplot as plt
    
    import numpy as np
    import numpy.linalg
    from MDAnalysis.analysis.dihedrals import Ramachandran
    import MDAnalysis as mda
    from MDAnalysis.lib.distances import calc_dihedrals
    
    
    import numpy.linalg
    import numpy as np
    
    import seaborn as sns
    from collections import namedtuple
    
    
    # In[2]:
    
    
    import numpy.linalg
    
    pdb = "step3_charmm2omm.pdb"
    dcd = "step5_1.dcd"
    rgyr_selection = 'segid PROF and backbone'
    
    u = mda.Universe(pdb, dcd)        # always start with a Universe
    nterm = u.PROF.atoms.N[0]   # can access structure via segid (s4AKE) and atom name
    cterm = u.PROF.atoms.C[-1]  # ... takes the last atom named 'C'
    bb = u.select_atoms('segid PROF and backbone')  # a selection (a AtomGroup)
    Rgyr = []
    D = []
    for ts in u.trajectory:     # iterate through all frames
      r = cterm.position - nterm.position # end-to-end vector from atom positions
      d = numpy.linalg.norm(r)  # end-to-end distance
      rgyr = bb.radius_of_gyration()  # method of a AtomGroup; updates with each frame
      Rgyr.append((u.trajectory.time, rgyr))
      D.append((u.trajectory.time, d))
      #print("frame = %d: d = %f Angstroem, Rgyr = %f Angstroem" % (ts.frame, d, rgyr))
    Rgyr = np.array(Rgyr)
    D = np.array(D)
    
    
    # In[3]:
    
    
    ax = plt.subplot(111)
    ax.plot(Rgyr[:,0], Rgyr[:,1], 'r-', lw=2, label=r"$R_G$")
    ax.set_xlabel("time (ps)")
    ax.set_ylabel(r"radius of gyration $R_G$ ($\AA$)")
    ax.figure.savefig("Rgyr.pdf")
    plt.draw()
    
    
    # In[4]:
    
    
    ay = plt.subplot(111)
    ay.plot(D[:,0], D[:,1], 'r-', lw=2, label=r"$R_D$")
    ay.set_xlabel("time (ps)")
    ay.set_ylabel(r"End to End distance ($\AA$)")
    ay.figure.savefig("D.pdf")
    plt.draw()
    
    
    # In[12]:
    
    
    ax = sns.distplot(Rgyr[:,1], vertical=True)
    ax.set_xlabel("time (ps)")
    ax.set_ylabel(r"radius of gyration $R_G$ ($\AA$)")
    
    
    # In[13]:
    
    
    import seaborn as sns, numpy as np
    ay = sns.distplot(D[:,1], vertical=True)
    ay.set_xlabel("time (ps)")
    ay.set_ylabel(r"End to End distance ($\AA$)")
    
    
    # In[ ]:
    
    
    
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

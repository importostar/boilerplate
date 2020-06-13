---
title: subsuper_issue
date: 2020-05-07
---
Example Python program subsuper_issue.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import matplotlib
* import matplotlib.pyplot as plt
* import sys
* import numpy as np

## Code

Python example

    #!/usr/bin/env python3
    import matplotlib
    import matplotlib.pyplot as plt
    import sys
    
    print('Matplotlib path: ', matplotlib.__path__, 'version: ', matplotlib.__version__)
    
    for fs in [None,'dejavusans','dejavuserif','cm','stix','stixsans']:
    #for fs in [None,'dejavuserif','cm','stix','stixsans','tex','texsans','texhelvet']:
        matplotlib.rcdefaults()
        if fs is None:
            fs = 'default'
        elif 'tex' in fs:
            plt.rcParams['text.usetex']=True
            #plt.rcParams['text.dvipnghack']=True
            if fs == 'texsans':
                plt.rcParams['text.latex.preamble'] = [r'\usepackage{arevtext,arevmath}']
            elif fs == 'texhelvet':
                plt.rcParams['text.latex.preamble'] = [r'\usepackage{sansmath}',
                                                       r'\sansmath',]
        else:
            plt.rcParams['mathtext.fontset']=fs
            #if fs == 'dejavuserif':
                #plt.rcParams['font.family'] = 'serif'
    
        f=plt.figure(figsize=(3.5,4.5))
        strings = [
                r'$\mathrm{EE^5E_5E^5_5E^5E} \quad E_\mathrm{cm} E_\mathrm{cm}^{3} E^\mathrm{e}_\mathrm{max}$',
                r'$F^2E_0E^5_5E^9\mathrm{E} \quad E_5\mathrm{E_5}{}_5$',
                r'$d^2 \leq K^2(q^2 - q_0^2)$',
                r'${}_2^3 y^a_b f^a_b g^a_b E_i^{0}E_i^aE_i^jE_{ij}E_{ij}^iE$',
                r'$E_i^{0}E_i^aE_i^jE_{ij}E_j^i{E}_j^iE$',
                r'$xyz^kx_kx^2y^{p-2} \quad d_i^jb_jc_kd^p \quad x^j_i E^0 E^0_u$',
                r'${xyz}^k{x}_{k}{x}^{2}{y}^{p-2} \quad {d}_{i}^{j}{b}_{j}{c}_{k}{d}^p \quad {x}^{j}_{i}{E}^{0}{E}^0_u$',
                r'f$^2$ f${}^2_3$ E${}^j_i$ $E^2\mathrm{E^2f^2f^9} f^2 f^\prime f^{\prime\prime}\mathrm{f^\prime f^{\prime\prime}}f\prime f^afaf2f9$',
                r'${\int}_\alpha^\beta x\oint_0^\infty x\int_{1}^{x}x\int_x x \int^x x \int_{x} x\int^{x}{\int}_{x} x{\int}^{x}_{x}x$',
                ]
    
        import numpy as np
    
        for s,p in zip(strings,np.linspace(0.,1.,len(strings)+2)[1:-1][::-1]):
                f.text(0.5,p,s,ha='center',va='center',size=12)
    
        f.text(0.03,0.9,'fontset: {0}'.format(fs),ha='left',va='top',
                rotation=90)
        f.savefig('subsup_test_mpl_{0}.png'.format(fs),dpi=150)
    
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

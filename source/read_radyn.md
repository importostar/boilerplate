---
title: read_radyn
date: 2020-05-07
---
Example Python program read_radyn.py

## Modules

* import radynpy

## Code

Python example

    import radynpy
    h = radynpy.RadynCdfLoader.load_vars('./radyn_out.cdf',varList = [])
    #h = radynpy.RadynCdfLoader.lazy_load_all ('./radyn_out.cdf',varList = [])
    
    #common varList
    #'z1': ('z1[t,k]', 'interface heights')
    #'vz1': ('vz1[t,k]', 'macroscopic velocity')
    #'d1': ('d1[t,k]', 'density')
    #'tg1': ('tg1[t,k]', 'temperature')
    #'n1': ('n1[t,k,i,iel]', 'population density in cm-3')
    #'ne1': ('ne1[t,k]', 'electron density')
    #'pg1': ('pg1[t,k]', 'gas pressure')
    #'en1': ('en1[t,k]', 'internal energy')
    #'coolt1': ('coolt1[t,k]', 'total cooling')
    #'cool': ('cool[t,k,kr]', 'cooling per transition/continuum in erg.cm-3.s-1')
    #'c': ('c[t,k,i,j,iel]', 'collisional transition rate'), 'heat1': ('heat1[t,k]', 'mechanical energy needed to sustain initial atmosphere')
    #'eion1': ('eion1[t,k]', 'ionization+excitation energy')
    #'outint': ('outint[t,nu,mu,kr]', 'monochromatic surface intensity in cgs units\nin nu=0 the continuum intensity is stored\nin nu=1:nq[kr] outint for the nu-points of the transition')
    #'cmass1': ('cmass1[t,k]', 'column mass at interface')
    #'dnyd': ('dnyd[t,k,iel]', 'doppler width in units of a typical doppler width')
    #'adamp': ('adamp[t,k,kr]', 'voigt damping parameter')
    #'z0': ('z0[t,k]', 'interface height at previous timestep')
    #'tau': ('tau[t,k]', 'opacity')
    #'vz0': ('vz0[t,k]', 'velocity at previous timestep')
    #'itime': ('itime[t]', 'timestep number'), 'time': ('time[t]', 'time')
    #'dtn': ('dtn[t]', 'timestep size from current to next time'), 'dtnm': ('dtnm[t]', 'timestep size from old to current time')
    #'zm': ('zm[t,k]', 'height for column masses of original gridpoints')
    #'nstar': ('nstar[t,k,i,iel]', 'lte population density')
    #'sl': ('sl[t,k,kr]', 'line source function')
    #'bp': ('bp[t,k,kr]', 'planck function')
    #'rij': ('rij[t,k,kr]', 'radiative rate from i to j per ni atom')
    #'rji': ('rji[t,k,kr]', 'radiative rate from j to i per nj atom')
    #'bheat1': ('bheat1[t,k]', 'beam heating in erg/s/cm3')

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

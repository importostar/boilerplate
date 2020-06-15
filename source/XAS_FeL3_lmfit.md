---
title: XAS_FeL3_lmfit
date: 2020-05-07
---
Example Python program XAS_FeL3_lmfit.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import numpy as np
* from lmfit.models import GaussianModel, ExponentialModel, PolynomialModel
* import matplotlib.pyplot as plt
* import xpspy as xpy

## Code

Python example

    import numpy as np
    from lmfit.models import GaussianModel, ExponentialModel, PolynomialModel
    import matplotlib.pyplot as plt
    import xpspy as xpy
    
    dat = np.loadtxt('130310_2254_FeL3.txt', skiprows = 1)
    
    x0 = dat[:, 0]
    y0 = dat[:, 1]
    
    xmin = 702
    xmax = 714
    
    [x, y] = xpy.fit_range(x0, y0, xmin, xmax)
    
    #bg_mod = ExponentialModel(prefix='bg_')
    #pars = bg_mod.guess(y, x=x)
    #bg_mod = PolynomialModel(3, prefix='bg_')
    #pars = bg_mod.guess(y, x=x)
    
    x_bg = xpy.shirley_calculate(x, y, 1e-5, 10)
    y = y - x_bg
    # x_bg = xpy.tougaard_calculate(x, y, 2866, 1643, 1, 1)
    # y = y - x_bg
    
    gauss1  = GaussianModel(prefix='g1_')
    pars = gauss1.make_params()
    #pars.update( gauss1.make_params())
    pars['g1_center'].set(707)
    pars['g1_sigma'].set(0.94, min=0.2, max=4)
    pars['g1_amplitude'].set(10, min=0)
    
    gauss2  = GaussianModel(prefix='g2_')
    pars.update( gauss2.make_params())
    pars['g2_center'].set(710)
    pars['g2_sigma'].set(1.15, min=0.2, max=4)
    pars['g2_amplitude'].set(5, min=0)
    
    # mod = gauss1 + gauss2 + bg_mod
    mod = gauss1 + gauss2
    
    init = mod.eval(pars, x=x)
    out = mod.fit(y, pars, x=x)
    comps = out.eval_components(x=x)
    # print(out.fit_report(min_correl=0.5))
    
    %matplotlib notebook
    # %matplotlib inline
    plt.figure(1)
    
    plt.xlabel('Photon energy (eV)')
    plt.ylabel('Intensity (arb units)')
    
    plt.plot(x0, y0, 'bo')
    # plt.plot(x, y+x_bg, 'bo')
    plt.plot(x, init + x_bg, 'k:')
    plt.plot(x, out.best_fit + x_bg, 'r-')
    plt.fill_between(x, comps['g1_'] + x_bg,  x_bg, color="#68d7e8")
    plt.fill_between(x, comps['g2_'] + x_bg,  x_bg, color="#e8b168")
    #plt.plot(x, comps['g1_'], 'm--')
    #plt.plot(x, comps['g2_'], 'm--')
    #plt.plot(x, comps['x_'], 'g-.')
    plt.plot(x, x_bg, 'g-.')
    
    # dely = out.eval_uncertainty(sigma=5)
    # plt.fill_between(x, out.best_fit-dely + x_bg, out.best_fit+dely + x_bg, color='#888888')
    
    plt.show()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

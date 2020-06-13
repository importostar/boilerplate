---
title: XPS_O1s_lmfit
date: 2020-05-07
---
Example Python program XPS_O1s_lmfit.py
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
    
    dat = np.loadtxt('111216_0459_O1s.txt', skiprows = 1)
    
    x0 = dat[:, 0]
    y0 = dat[:, 1]
    
    xmin = 520
    xmax = 540
    
    [x, y] = xpy.fit_range(x0, y0, xmin, xmax)
    
    #bg_mod = ExponentialModel(prefix='bg_')
    #pars = bg_mod.guess(y, x=x)
    bg_mod = PolynomialModel(3, prefix='bg_')
    pars = bg_mod.guess(y, x=x)
    
    gauss1  = GaussianModel(prefix='g1_')
    pars.update( gauss1.make_params())
    pars['g1_center'].set(530, vary = False)
    pars['g1_sigma'].set(1.08, min=0.2, max=2)
    pars['g1_amplitude'].set(1.03, min=0)
    
    gauss2  = GaussianModel(prefix='g2_')
    pars.update( gauss2.make_params())
    pars['g2_center'].set(531.5, vary = False)
    pars['g2_sigma'].set(1.27, min=0.2, max=2)
    pars['g2_amplitude'].set(0.9, min=0)
    
    gauss3  = GaussianModel(prefix='g3_')
    pars.update( gauss3.make_params())
    pars['g3_center'].set(533.5, vary = False)
    pars['g3_sigma'].set(1.27, min=0.2, max=2)
    pars['g3_amplitude'].set(0.25, min=0)
    
    mod = bg_mod + gauss1 + gauss2 + gauss3
    
    init = mod.eval(pars, x=x)
    out = mod.fit(y, pars, x=x)
    comps = out.eval_components(x=x)
    # print(out.fit_report())
    
    %matplotlib notebook
    # %matplotlib inline
    plt.figure(1)
    
    plt.xlabel('Binding energy (eV)')
    plt.ylabel('Intensity (arb units)')
    
    plt.plot(x0, y0, 'bo')
    # plt.plot(x, y+x_bg, 'bo')
    plt.plot(x, init, 'k:')
    plt.plot(x, out.best_fit, 'r-')
    plt.fill_between(x, comps['g1_']+comps['bg_'], comps['bg_'], color="#68d7e8")
    plt.fill_between(x, comps['g2_']+comps['bg_'], comps['bg_'], color="#6895e8")
    plt.fill_between(x, comps['g3_']+comps['bg_'], comps['bg_'], color="#e8b168")
    #plt.plot(x, comps['g1_'], 'm--')
    #plt.plot(x, comps['g2_'], 'm--')
    #plt.plot(x, comps['g3_'], 'm--')
    #plt.plot(x, comps['bg_'], 'g-.')
    plt.plot(x, comps['bg_'], 'g-.')
    
    dely = out.eval_uncertainty(sigma=5)
    plt.fill_between(x, out.best_fit-dely, out.best_fit+dely, color='#888888')
    
    plt.gca().invert_xaxis()
    plt.show()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

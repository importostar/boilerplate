---
title: XPS_C1s_lmfit
date: 2020-05-07
---
Example Python program XPS_C1s_lmfit.py
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
    
    dat = np.loadtxt('120324_1144_C1s.txt', skiprows = 1)
    
    x0 = dat[:, 0]
    y0 = dat[:, 1]
    
    xmin = 280
    xmax = 295
    
    [x, y] = xpy.fit_range(x0, y0, xmin, xmax)
    
    #bg_mod = ExponentialModel(prefix='exp_')
    #pars = bg_mod.guess(y, x=x)
    #bg_mod = PolynomialModel(3, prefix='poly_')
    #pars = bg_mod.guess(y, x=x)
    
    #x_bg = xpy.shirley_calculate(x, y, 1e-5, 10)
    #y = y - x_bg
    x_bg = xpy.tougaard_calculate(x, y, 2866, 1643, 1, 1)
    y = y - x_bg
    
    gauss1  = GaussianModel(prefix='g1_')
    pars = gauss1.make_params()
    #pars.update( gauss1.make_params())
    pars['g1_center'].set(284.59, vary = False)
    pars['g1_sigma'].set(1.01, min=0.2, max=1.5)
    pars['g1_amplitude'].set(26.36, min=0)
    
    gauss2  = GaussianModel(prefix='g2_')
    pars.update( gauss2.make_params())
    pars['g2_center'].set(286, vary = False)
    pars['g2_sigma'].set(1.27, min=0.2, max=1.5)
    pars['g2_amplitude'].set(2.63, min=0)
    
    gauss3  = GaussianModel(prefix='g3_')
    pars.update( gauss3.make_params())
    pars['g3_center'].set(288.5, vary = False)
    pars['g3_sigma'].set(1.27, min=0.2, max=1.5)
    pars['g3_amplitude'].set(1.54, min=0)
    
    gauss4  = GaussianModel(prefix='g4_')
    pars.update( gauss4.make_params())
    pars['g4_center'].set(291.59, vary = False)
    pars['g4_sigma'].set(1.27, min=0.2, max=1.5)
    pars['g4_amplitude'].set(1.35, min=0)
    
    #mod = gauss1 + gauss2 + gauss3 + gauss4 + x_mod
    mod = gauss1 + gauss2 + gauss3 + gauss4
    
    init = mod.eval(pars, x=x)
    out = mod.fit(y, pars, x=x)
    comps = out.eval_components(x=x)
    # print(out.fit_report(min_correl=0.5))
    
    %matplotlib notebook
    # %matplotlib inline
    plt.figure(1)
    
    plt.xlabel('Binding energy (eV)')
    plt.ylabel('Intensity (arb units)')
    
    plt.plot(x0, y0, 'bo')
    # plt.plot(x, y+x_bg, 'bo')
    plt.plot(x, init+x_bg, 'k:')
    plt.plot(x, out.best_fit+x_bg, 'r-')
    plt.fill_between(x, comps['g1_']+x_bg, x_bg, color="#68d7e8")
    plt.fill_between(x, comps['g2_']+x_bg, x_bg, color="#6895e8")
    plt.fill_between(x, comps['g3_']+x_bg, x_bg, color="#e8b168")
    plt.fill_between(x, comps['g4_']+x_bg, x_bg, color="#e86897")
    #plt.plot(x, comps['g1_'], 'm--')
    #plt.plot(x, comps['g2_'], 'm--')
    #plt.plot(x, comps['g3_'], 'm--')
    #plt.plot(x, comps['g4_'], 'm--')
    #plt.plot(x, comps['bg_'], 'g-.')
    plt.plot(x, x_bg, 'g-.')
    
    # dely = out.eval_uncertainty(sigma=5)
    # plt.fill_between(x, out.best_fit-dely+x_bg, out.best_fit+dely+x_bg, color='#888888')
    
    plt.gca().invert_xaxis()
    plt.show()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

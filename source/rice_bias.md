---
title: rice_bias
date: 2020-05-07
---
Example Python program rice_bias.py

## Modules

* import numpy as np
* from scipy.special import iv
* from scipy.optimize import root_scalar
* import matplotlib.pyplot as plt
* import matplotlib

## Methods

* def func(p_real, p_obs, sigma):
* def find_true_p(p_obs, sigma_qu):

## Code

Python example

    import numpy as np
    from scipy.special import iv
    from scipy.optimize import root_scalar
    import matplotlib.pyplot as plt
    label_size = 16
    import matplotlib
    matplotlib.rcParams['xtick.labelsize'] = label_size
    matplotlib.rcParams['ytick.labelsize'] = label_size
    matplotlib.rcParams['axes.titlesize'] = label_size
    matplotlib.rcParams['axes.labelsize'] = label_size
    matplotlib.rcParams['font.size'] = label_size
    matplotlib.rcParams['legend.fontsize'] = label_size
    matplotlib.rcParams['pdf.fonttype'] = 42
    matplotlib.rcParams['ps.fonttype'] = 42
    
    
    def func(p_real, p_obs, sigma):
        return iv(0, p_obs*p_real/sigma**2)*(1 - (p_obs/sigma)**2) + iv(1, p_obs*p_real/sigma**2)*p_obs*p_real/sigma**2
    
    
    def find_true_p(p_obs, sigma_qu):
        res = root_scalar(func, args=(p_obs, sigma_qu,), bracket=(0, p_obs))
        return res.root
    
    
    sigma = 1
    p_obs = np.linspace(1, 5, 100)
    p_reals = list()
    p_corr = list()
    for p_o in p_obs:
        snr = p_o/sigma
        factor = 1-1/snr**2
        if factor < 0:
            factor = 0
        p_corr.append(p_o*np.sqrt(factor))
    p_corr = np.array(p_corr)
    
    for p_o in p_obs:
        p_reals.append(find_true_p(p_o, sigma))
        
    p_reals = np.array(p_reals)
    plt.plot(p_reals/sigma, p_obs/sigma, color="r", lw=2, label="exact")
    plt.plot(p_corr/sigma, p_obs/sigma, color="g", label="approx")
    plt.legend()
    plt.xlim([0, 3])
    plt.ylim([0, 3])
    plt.xlabel(r"$p_{\rm true}/\sigma$")
    plt.ylabel(r"$p_{\rm obs}/\sigma$")
    x = np.linspace(0, 5, 100)
    plt.plot(x, x, color="k")
    plt.show()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

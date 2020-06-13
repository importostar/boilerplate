---
title: secondary_axis
date: 2020-05-07
---
Example Python program secondary_axis.py

## Modules

* import matplotlib.pyplot as plt
* import numpy as np
* import datetime
* import matplotlib.dates as mdates
* from matplotlib.transforms import Transform
* from matplotlib.ticker import (

## Methods

* def deg2rad(x):
* def rad2deg(x):
* def forward(x):
* def inverse(x):
* def date2yday(x):
* def yday2date(x):
* def CtoF(x):
* def FtoC(x):
* def mtof(x):
* def ftom(x):

## Code

Python example

    %matplotlib inline
    
    import matplotlib.pyplot as plt
    import numpy as np
    import datetime
    import matplotlib.dates as mdates
    from matplotlib.transforms import Transform
    from matplotlib.ticker import (
        AutoLocator, AutoMinorLocator)
    
    fig, ax = plt.subplots(constrained_layout=True)
    x = np.arange(0, 360, 1)
    y = np.cos(2 * x * np.pi / 180)
    ax.plot(x, y)
    ax.set_xlabel('angle [degrees]')
    ax.set_ylabel('signal')
    ax.set_title('Cosine wave')
    
    
    def deg2rad(x):
        return x * np.pi / 180
    
    def rad2deg(x):
        return x * 180 / np.pi
    
    
    secax = ax.secondary_xaxis('top', functions=(deg2rad, rad2deg))
    secax.set_xlabel('angle [rad]')
    #plt.savefig('cos_xsecondary.jpg',dpi=100)
    plt.show()
    
    
    #log-log
    fig, ax = plt.subplots(constrained_layout=True)
    x = np.linspace(0.02, 1, 50)
    y = np.random.randn(len(x)) ** 2
    ax.loglog(x, y)
    ax.set_xlabel('f [Hz]')
    ax.set_ylabel('PSD')
    ax.set_title('Random spectrum')
    
    
    def forward(x):
        return 1 / x
    
    
    def inverse(x):
        return 1 / x
    
    secax = ax.secondary_xaxis('top', functions=(forward, inverse))
    secax.set_xlabel('period [s]')
    plt.savefig('random_xsecondary.jpg',dpi=100)
    plt.show()
    
    
    #rime & F
    dates = [datetime.datetime(2018, 1, 1) + datetime.timedelta(hours=k * 6)
                for k in range(240)]
    temperature = 20 + np.random.randn(len(dates))
    fig, ax = plt.subplots(constrained_layout=True)
    
    ax.plot(dates, temperature)
    ax.set_ylabel(r'$T\ [^oC]$')
    plt.xticks(rotation=70)
    
    
    def date2yday(x):
        """
        x is in matplotlib datenums, so they are floats.
        """
        y = x - mdates.date2num(datetime.datetime(2018, 1, 1))
        return y
    
    
    def yday2date(x):
        """
        return a matplotlib datenum (x is days since start of year)
        """
        y = x + mdates.date2num(datetime.datetime(2018, 1, 1))
        return y
    
    secaxx = ax.secondary_xaxis('top', functions=(date2yday, yday2date))
    secaxx.set_xlabel('yday [2018]')
    
    
    def CtoF(x):
        return x * 1.8 + 32
    
    
    def FtoC(x):
        return (x - 32) / 1.8
    
    secaxy = ax.secondary_yaxis('right', functions=(CtoF, FtoC))
    secaxy.set_ylabel(r'$T\ [^oF]$')
    #plt.savefig('datetime_do.jpg',dpi=100)
    plt.show()
    
    
    #feet&meter
    fig, ax = plt.subplots()
    x = np.linspace(0, 50, 51)
    y = np.random.randn(len(x)) ** 2
    ax.plot(x, y,'k-')
    ax.set_xlabel('distance / m')
    
    
    def mtof(x):
        return x * 3.2808
    
    
    def ftom(x):
        return x / 3.2808
    
    secax = ax.secondary_xaxis('top', functions=(mtof, ftom))
    secax.set_xlabel('distance / feet')
    #plt.savefig('distance_xsecondary.jpg',dpi=100)
    plt.show()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

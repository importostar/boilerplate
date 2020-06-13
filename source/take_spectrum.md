---
title: take_spectrum
date: 2020-05-07
---
Example Python program take_spectrum.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import numpy as np
* import seabreeze.spectrometers as sb
* import matplotlib.pyplot as plt
* import matplotlib.animation as animation
* import matplotlib.gridspec as gridspec
* from matplotlib.widgets import Slider
* import time
* import datetime
* import pytz

## Methods

* def update_line(y):
* def data_gen():

## Code

Python example

    import numpy as np
    import seabreeze.spectrometers as sb
    import matplotlib.pyplot as plt
    import matplotlib.animation as animation
    import matplotlib.gridspec as gridspec
    from matplotlib.widgets import Slider
    import time
    import datetime
    import pytz
    
    # open device
    device = sb.list_devices()[0]
    print('using device:', device)
    spec = sb.Spectrometer(device)
    spec.integration_time_micros(spec.minimum_integration_time_micros)
    
    # according to this documentation:
    # https://oceanoptics.com/wp-content/uploads/OEM-Data-Sheet-USB2000-.pdf
    # pixels 0-19 are not exposed to incoming light
    # they are used for internal standards, including automatic dark count compensation
    # we ignore these indicies here
    wl = spec.wavelengths()[20:]
    
    # prepare animated figure
    fig = plt.figure()
    gs = gridspec.GridSpec(2, 1, height_ratios=[10, 1])
    ax = plt.subplot(gs[0])
    hl, = plt.plot(wl, spec.intensities(correct_dark_counts=True, correct_nonlinearity=True)[20:])
    plt.ylim(-100, 4096)
    def update_line(y):
        hl.set_ydata(y)
        plt.draw()
    def data_gen():
        while True:
            yield spec.intensities(correct_dark_counts=True, correct_nonlinearity=True)[20:]
    
    # add slider to change integration time
    ax = plt.subplot(gs[1])
    slider = Slider(ax, "integration time", spec.minimum_integration_time_micros, 1e6, valinit=5000)
    slider.on_changed(spec.integration_time_micros)
    
    # run animation
    ani = animation.FuncAnimation(fig, update_line, data_gen, interval=100)
    plt.show()
    
    # once the figure is closed, run the following and exit
    # technically, this is a separate acquisition from the final dispayed spectrum
    d = datetime.datetime.utcnow()
    d_with_timezone = d.replace(tzinfo=pytz.UTC)
    ts = d_with_timezone.isoformat()
    intensities = spec.intensities(correct_dark_counts=True, correct_nonlinearity=True)
    with open("%s.txt" % ts, 'w+') as f:
        headers = []
        headers += ["timestamp:\t" + ts]
        headers += ["make:\tOcean Optics"]
        headers += ["model:\t" + spec.model]
        headers += ["serial:\t" + device.serial]
        headers += ["subtracted dark counts:\t" + "%d" % -intensities[0]]
        headers += ["columns: wavelength (nm)\tcounts"]
        np.savetxt(f, np.stack([wl, intensities[20:]], 1), fmt=["%8.6f", "%d"], delimiter='\t',
                header='\n'.join(headers))
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

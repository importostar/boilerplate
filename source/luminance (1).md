---
title: luminance (1)
date: 2020-05-07
---
Example Python program luminance (1).py

## Modules

* import numpy as N
* import matplotlib.colors
* from matplotlib import pyplot as P
* from matplotlib import cbook

## Methods

* def rotate(x, y, angle):
* def luminance_colormap(num_cycles=2, num_colors=256, reverse=False):

## Code

Python example

    import numpy as N
    import matplotlib.colors
    
    
    def rotate(x, y, angle):
        r, theta = N.sqrt(x ** 2 + y ** 2), N.arctan2(y, x)
        theta += angle
        return r * (N.cos(theta), N.sin(theta))
    
    
    def luminance_colormap(num_cycles=2, num_colors=256, reverse=False):
        '''Returns a Matplotlib color scale that cycles through the hues @num_cycles
        times, while maintaining monotonic luminance (i.e., if it is printed in
        black and white, then it will be perceptually equal to a linear grayscale.
    
        Ported from the Matlab(R) code from: McNames, J. (2006). An effective color
        scale for simultaneous color and gray-scale publications. IEEE Signal
        Processing Magazine 23(1), 82--87.'''
    
        # Triangular window function
        window = N.sqrt(3.0 / 8.0) * N.bartlett(num_colors)
    
        # Independent variable
        t = N.linspace(N.sqrt(3.0), 0.0, num_colors)
    
        # Initial values
        operand = (t - N.sqrt(3.0) / 2.0) * num_cycles * 2.0 * N.pi / N.sqrt(3.0)
        r0 = t
        g0 = window * N.cos(operand)
        b0 = window * N.sin(operand)
    
        # Convert RG to polar, rotate, and convert back
        r1, g1 = rotate(r0, g0, N.arcsin(1.0 / N.sqrt(3.0)))
        b1 = b0
    
        # Convert RB to polar, rotate, and convert back
        r2, b2 = rotate(r1, b1, N.pi / 4.0)
        g2 = g1
    
        # Ensure finite precision effects don't exceed unit cube boundaries
        r = r2.clip(0.0, 1.0)
        g = g2.clip(0.0, 1.0)
        b = b2.clip(0.0, 1.0)
    
        the_map = N.vstack((r, g, b)).T
        return matplotlib.colors.ListedColormap(the_map[::-1 if reverse else 1])
    
    if __name__ == '__main__':
        from matplotlib import pyplot as P
        from matplotlib import cbook
    
        w, h = 512, 512
        datafile = cbook.get_sample_data('ct.raw', asfileobj=False)
        s = file(datafile, 'rb').read()
        A = N.fromstring(s, N.uint16).astype(float)
        A /= max(A)
        A.shape = w, h
        extent = (0, 25, 0, 25)
    
        fig = P.figure()
        ax = fig.add_subplot(1, 1, 1)
        im = ax.imshow(A, cmap=luminance_colormap(), origin='upper', extent=extent)
        fig.colorbar(im)
        P.show()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

---
title: myNorm
date: 2020-05-07
---
Example Python program myNorm.py

## Modules

* import matplotlib.colors
* import matplotlib.pyplot
* import numpy as np

## Classes

* class myNorm(matplotlib.colors.Normalize):

## Methods

* def __init__(self, vmin=None, vmax=None, clip=False,tfunc = lambda x:x):
* def __call__(self, value, clip=None):

## Code

Python example

    #!/usr/bin/env python3
    # -*- coding: utf-8 -*-
    
    import matplotlib.colors
    
    class myNorm(matplotlib.colors.Normalize):
        def __init__(self, vmin=None, vmax=None, clip=False,tfunc = lambda x:x):
            self.tfunc = tfunc
            return super().__init__(vmin,vmax,clip)
        def __call__(self, value, clip=None):
            'most of this is copied straight from matplotlib.colors.LogNorm'
            if clip is None:
                clip = self.clip
    
            result, is_scalar = self.process_value(value)
    
            result = np.ma.masked_less_equal(result, 0, copy=False)
    
            self.autoscale_None(result)
            vmin, vmax = self.vmin, self.vmax
            if vmin > vmax:
                raise ValueError("minvalue must be less than or equal to maxvalue")
            elif vmin <= 0:
                raise ValueError("values must all be positive")
            elif vmin == vmax:
                result.fill(0)
            else:
                if clip:
                    mask = np.ma.getmask(result)
                    result = np.ma.array(np.clip(result.filled(vmax), vmin, vmax),
                                         mask=mask)
                # in-place equivalent of above can be much faster
                resdat = result.data
                mask = result.mask
                if mask is np.ma.nomask:
                    mask = (resdat <= 0)
                else:
                    mask |= resdat <= 0
                np.copyto(resdat, 1, where=mask)
                resdat = self.tfunc(resdat)
                resdat -= self.tfunc(vmin)
                resdat /= (self.tfunc(vmax) - self.tfunc(vmin))
                result = np.ma.array(resdat, mask=mask, copy=False)
            if is_scalar:
                result = result[0]
            return result
    
    if __name__=='__main__':
        import matplotlib.pyplot
        import numpy as np
        matplotlib.pyplot.pcolormesh(
                np.random.lognormal(1.,1.,[100,100]),
                norm=myNorm(tfunc=lambda x:np.log(1+x))
                )
        matplotlib.pyplot.waitforbuttonpress()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

---
title: dct_test
date: 2020-05-07
---
Example Python program dct_test.py

## Modules

* import numpy as np
* from scipy.fftpack import dct, idct
* import matplotlib.pyplot as plt
* from PIL import Image
* import matplotlib.image

## Methods

* def dct_2d(x):
* def idct_2d(x):
* def compress(image, n):
* def discrete(image):

## Code

Python example

    import numpy as np
    from scipy.fftpack import dct, idct
    import matplotlib.pyplot as plt
    from PIL import Image
    import matplotlib.image
    
    def dct_2d(x):
        return dct(dct(x, axis=0, norm='ortho'), axis=1, norm='ortho')
    
    def idct_2d(x):
        return idct(idct(x, axis=0 , norm='ortho'), axis=1 , norm='ortho')
    
    def compress(image, n):
        w = np.zeros_like(image)
        w[0:n, 0:n, :] = 1
        k = dct_2d(image) * w
        return idct_2d(k)
    
    def discrete(image):
        r0 = (image[:, :, 0] > image[:, :, 1]).astype(float) * (image[:, :, 0] > image[:, :, 2]).astype(float)
        r1 = (image[:, :, 1] > image[:, :, 0]).astype(float) * (image[:, :, 1] > image[:, :, 2]).astype(float)
        r2 = (image[:, :, 2] > image[:, :, 0]).astype(float) * (image[:, :, 2] > image[:, :, 1]).astype(float)
        return np.dstack([r0, r1, r2])
    
      
    image = matplotlib.image.imread("1.png")
    
    for i in range(1, 200):
        result = discrete(compress(image, i))
        matplotlib.image.imsave(f"v/{i:03}.png", result)

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

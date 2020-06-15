---
title: compare
date: 2020-05-07
---
Example Python program compare.py

## Modules

* import matplotlib
* import skimage.measure
* import matplotlib.pyplot
* import matplotlib.image

## Methods

* def compare_images(imageFileA, imageFileB, title):

## Code

Python example

    # http://www.pyimagesearch.com/2014/09/15/python-compare-two-images/
    # scikit-image: http://scikit-image.org
    # pip3 install -U scikit-image
    
    import matplotlib
    matplotlib.use('TkAgg')
    
    import skimage.measure
    import matplotlib.pyplot
    import matplotlib.image
    
    def compare_images(imageFileA, imageFileB, title):
        # load the images
        imageA = matplotlib.image.imread(imageFileA)
        imageB = matplotlib.image.imread(imageFileB)
    
        # http://scikit-image.org/docs/stable/api/skimage.measure.html
        n = skimage.measure.compare_nrmse(imageA, imageB)
        p = skimage.measure.compare_psnr(imageA, imageB)
        s = skimage.measure.compare_ssim(imageA, imageB, multichannel=True)
    
        # setup the figure
        fig = matplotlib.pyplot.figure(title, figsize=(7, 7))
        matplotlib.pyplot.suptitle("NRMSE: %.2f, PSNR: %.2f, SSIM: %.2f" % (n, p, s))
    
        # show first image
        ax = fig.add_subplot(1, 2, 1)
        matplotlib.pyplot.imshow(imageA)
        matplotlib.pyplot.axis("off")
    
        # show the second image
        ax = fig.add_subplot(1, 2, 2)
        matplotlib.pyplot.imshow(imageB)
        matplotlib.pyplot.axis("off")
    
        # show the images
        matplotlib.pyplot.show()
    
    # compare the images
    compare_images("images/apple.jpg", "images/orange.jpg", "Original vs. Contrast")
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

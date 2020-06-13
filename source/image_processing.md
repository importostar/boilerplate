---
title: image_processing
date: 2020-05-07
---
Example Python program image_processing.py

## Modules

* from scipy.signal import convolve2d
* from scipy import ndimage
* import Image
* from scipy.ndimage import filters 

## Code

Python example

    # Read and display image
    upf = imread("upf.png")
    imshow(upf)
    
    # Convert to grayscayle and display upright
    upf_grey = mean(upf, cmap=cm.gray)
    imshow(upf_grey)
    
    # Make a cheap line filter
    sobel_h = array([[1,2,1], [0,0,0], [-1,-2,-1]])
    sobel_v = sobel_h.transpose()
    from scipy.signal import convolve2d
    edges_h = convolve2d(upf_grey, sobel_h)
    edges_v = convolve2d(upf_grey, sobel_v)
    edges = hypot(edges_h, edges_v)
    imshow(edges)
    
    # But actually, scipy does that:
    from scipy import ndimage
    edges_h = ndimage.sobel(upf_grey, axis=0)
    edges_v = ndimage.sobel(upf_grey, axis=1)
    edges = hypot(edges_h, edges_v)
    imshow(edges)
    
    # make a feature-mappy thing
    edge_feature = ndimage.gaussian_filter(edges, 10)
    imshow(edge_feature)
    
    import Image
    luminance = Image.fromarray(upf_grey).convert('L')
    luminance_feature = ndimage.gaussian_filter(luminance, 10)
    imshow(luminance_feature)
    
    attention = 0.3 * luminance_feature + 0.7 * edge_feature
    imshow(attention)
    
    from scipy.ndimage import filters 
    maxima = filters.maximum_filter(attention, 10) 
    minima = filters.minimum_filter(attention, 10) 
    diff = (maxima - minima > 25)  * 1.0 # arbitrary threshold 
    maxima_smooth = ndimage.gaussian_filter(diff, 15) 
    imshow(maxima_smooth)
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

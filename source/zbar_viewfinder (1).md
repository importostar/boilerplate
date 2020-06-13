---
title: zbar_viewfinder (1)
date: 2020-05-07
---
Example Python program zbar_viewfinder (1).py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import zbar
* import skimage.io
* import skimage.transform
* import skimage.color
* import numpy as np
* import argparse
* import sys
* import matplotlib.pyplot as plt
* import matplotlib

## Classes

* class ViewFinder(object):

## Methods

* 	def __init__(self, image, fig_whole, fig_view):
* 	def update_cb(self, draw_event):
* 	def set_crop(self):
* 	def draw_viewfinder(self):
* 	def save(self, filename):

## Code

Python example

    import zbar
    import skimage.io
    import skimage.transform
    import skimage.color
    
    import numpy as np
    
    import argparse
    import sys
    
    import matplotlib.pyplot as plt
    import matplotlib
    
    
    """
    start ipython
    enter %matplotlib
    enter %run zbar_viewfinder --input scan-266.jpg
    optionally enter  `vf.downsample_factor = 2` or some other downsample factor.
    pan/zoom figure 1, click on image. confirm that the view is updated on figure 2, and look for any decoded output on stdout
    """
    
    qr_scanner = zbar.Scanner()
    
    parser = argparse.ArgumentParser(
    	description="look for QR codes in matplotlib viewfinder")
    
    parser.add_argument(
    	'--input', type=argparse.FileType('br'),
    	help='an input image.')
    
    args = parser.parse_args()
    
    input_image = skimage.io.imread(args.input)
    
    
    class ViewFinder(object):
    	def __init__(self, image, fig_whole, fig_view):
    		self.image = image
    		self.image_shape = self.image.shape[0:2] # don't care about color/alpha channels
    		self.fig_whole = fig_whole
    		self.fig_view = fig_view
    		self.ax_whole = self.fig_whole.add_subplot(1,1,1)
    		self.ax_view = self.fig_view.add_axes([0,0,1,1])
    
    		self.ax_whole.set_title("zoom/pan and then click on image to update viewfinder")
    		self.ax_view.set_title("viewfinder")
    		self.crop = [ (0, s) for s in self.image_shape]
    		self.downsample_factor = 1
    		self.rotation = 0.0
    
    		self.ax_whole.imshow(self.image)
    		self.ax_whole.set_axis_bgcolor("yellow")
    		self.fig_whole.canvas.mpl_connect('button_press_event', self.update_cb)
    
    		self.update_cb(None) # force initial draw
    
    
    	def update_cb(self, draw_event):
    		self.set_crop()
    		self.draw_viewfinder()
    
    
    	def set_crop(self):
    		crop = [self.ax_whole.get_ylim(), self.ax_whole.get_xlim()]
    		crop = [ tuple([int(a) for a in b]) for b in crop]
    		crop_coerce = [ tuple([min(max(_min, v), _max) for v in b]) for (b,_min,_max) in zip(crop, [0,0], self.image_shape)]
    		self.crop = crop_coerce
    		print("crop: {}".format(self.crop))
    
    
    	def draw_viewfinder(self):
    		c = self.crop
    		cropped = self.image[c[0][1]:c[0][0],c[1][0]:c[1][1],:]
    
    		if len(cropped.shape) == 3:
    			cropped = skimage.color.rgb2gray(cropped)
    
    		rotated = skimage.transform.rotate(cropped, self.rotation)
    
    		downsampled = skimage.transform.downscale_local_mean(rotated, (self.downsample_factor, self.downsample_factor))
    		page_as_u8 = skimage.img_as_ubyte(downsampled)
    		self.ax_view.imshow(page_as_u8, interpolation="nearest", cmap=matplotlib.cm.binary_r)
    
    		barcodes = qr_scanner.scan(page_as_u8)
    		print(barcodes)
    
    		self.last_scanned = page_as_u8
    		self.ax_view.figure.canvas.draw()
    
    	def save(self, filename):
    		skimage.io.imsave(filename, self.last_scanned)
    
    
    
    fig1 =  plt.figure()
    fig2 = plt.figure()
    
    vf = ViewFinder(input_image, fig1, fig2)
    
    plt.show()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

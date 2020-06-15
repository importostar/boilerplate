---
title: rectangle_selector_example
date: 2020-05-07
---
Example Python program rectangle_selector_example.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import numpy as np
* import matplotlib.pyplot as plt
* from matplotlib.widgets import RectangleSelector
* import fibsem

## Methods

* def _select_rectangle_callback(eclick, erelease):
* def toggle_selector(event):
* def select_rectangle(image):
* def quick_plot(image):
* def main():

## Code

Python example

    import numpy as np
    import matplotlib.pyplot as plt
    from matplotlib.widgets import RectangleSelector
    
    
    def _select_rectangle_callback(eclick, erelease):
        """eclick and erelease are the press and release events"""
        x1, y1 = eclick.xdata, eclick.ydata
        x2, y2 = erelease.xdata, erelease.ydata
    
    
    def toggle_selector(event):
        """Matplotlib interactive selection."""
        if event.key in ['Q', 'q'] and toggle_selector.RS.active:
            toggle_selector.RS.set_active(False)
        if event.key in ['A', 'a'] and not toggle_selector.RS.active:
            toggle_selector.RS.set_active(True)
    
    
    def select_rectangle(image):
        """Return location of interactive user click on image.
    
        Parameters
        ----------
        image : AdornedImage or 2D numpy array.
    
        Returns
        -------
        center, extents
              Rectangle center and extents.
              Coordinates are in x, y format & real space units.
              (Units are the same as the matplotlib figure axes.)
              Rectangle extents are given as: (xmin, xmax, ymin, ymax).
        """
        fig, ax = quick_plot(image)
        # Here are the docs fir the matplotlib RectangleSelector
        # https://matplotlib.org/3.1.0/api/widgets_api.html#matplotlib.widgets.RectangleSelector
        toggle_selector.RS = RectangleSelector(ax, _select_rectangle_callback,
                                               drawtype='box', useblit=True,
                                               # don't use middle button
                                               button=[1, 3],
                                               minspanx=5, minspany=5,
                                               spancoords='pixels',
                                               interactive=True)
        plt.show()
        center = toggle_selector.RS.center  # xy coord, units same as plot axes
        extents = toggle_selector.RS.extents  # Return (xmin, xmax, ymin, ymax)
        return center, extents
    
    
    def quick_plot(image):
        """Display image with matplotlib.pyplot
    
        Parameters
        ----------
        image : Adorned image or numpy array
            Input image.
    
        Returns
        -------
        fig, ax
            Matplotlib figure and axis objects.
        """
        fig, ax = plt.subplots(1)
        display_image = image.data
        height, width = display_image.shape
        try:
            pixelsize_x = image.metadata.binary_result.pixel_size.x
            pixelsize_y = image.metadata.binary_result.pixel_size.y
        except AttributeError:
            extent_kwargs = [-(width / 2), +(width / 2),
                             -(height / 2), +(height / 2)]
            ax.set_xlabel('Distance from origin (pixels)')
        else:
            extent_kwargs = [-(width / 2) * pixelsize_x,
                             +(width / 2) * pixelsize_x,
                             -(height / 2) * pixelsize_y,
                             +(height / 2) * pixelsize_y]
            ax.set_xlabel('Distance from origin (meters) \n'
                          '1 pixel = {} meters'.format(pixelsize_x))
        ax.set_xlim(extent_kwargs[0], extent_kwargs[1])
        ax.set_ylim(extent_kwargs[2], extent_kwargs[3])
        ax.imshow(display_image, cmap='gray', extent=extent_kwargs)
        return fig, ax
    
    
    def main():
        import fibsem
        rect_coords = select_rectangle(fibsem.data.embryo_adorned())
        print(rect_coords)
    
    
    if __name__ == '__main__':
        main()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

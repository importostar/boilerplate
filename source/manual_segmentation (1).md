---
title: manual_segmentation (1)
date: 2020-05-07
---
Example Python program manual_segmentation (1).py

## Modules

* import matplotlib.pyplot as plt

## Methods

* def select_line(image):

## Code

Python example

    import matplotlib.pyplot as plt
    
    
    def select_line(image):
        """Interactively select a line with matplotlib.
        
        Adapted from this StackOverflow answer by user dawe:
        https://stackoverflow.com/questions/9136938/matplotlib-interactive-graphing-manually-drawing-lines-on-a-graph
        
        Parameters
        ----------
        image : AdornedImage
    
        Returns
        -------
        line_coordinates
            Row, column format & units of pixels.
        """
        image = fibsem.conversions._convert_to_numpy(image)
        fig, ax = plt.subplots(1)
        ax.imshow(image, cmap='gray')
        ax = plt.gca()
        xy = plt.ginput(2)
        x = [p[0] for p in xy]
        y = [p[1] for p in xy]
        line = plt.plot(x, y, 'y')
        ax.figure.canvas.draw()
        line_coordinates = [(xy[0][1], xy[0][0]), (xy[1][1], xy[1][0])]
        return line_coordinates
    
    
    # Note that this deprecation warning is produced:
    # site-packages\matplotlib\backend_bases.py:2445: MatplotlibDeprecationWarning: Using default event loop until function specific to this GUI is implemented
    #   warnings.warn(str, mplDeprecation)

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

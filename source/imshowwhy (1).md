---
title: imshowwhy (1)
date: 2020-05-07
---
Example Python program imshowwhy (1).py

## Modules

* import scipy.misc
* import matplotlib as mpl
* import matplotlib.pyplot as plt
* import numpy as np

## Methods

* def make_image():

## Code

Python example

    # Read a grid in the native projection and display with matplotlib and scipy.
    import scipy.misc
    
    import matplotlib as mpl
    import matplotlib.pyplot as plt
    import numpy as np
    
    
    def make_image():
    
        dpi = 100.
    
        fig = plt.figure(figsize=(600/dpi, 900/dpi), dpi=dpi, edgecolor='none')
    
        image_axes = fig.add_axes([0, 0, 1, 1])
    
        landmask = 'resampled-mask.600x900.bin'
        grid = np.fromfile(landmask, dtype=np.uint8).reshape((900, 600))
        grid[grid == 101] = 0       # reset permanent ice to land
    
        ct_cmap, ct_norm = mpl.colors.from_levels_and_colors(
            [0, 50, 256], ['#000000', '#FFFFFF']
        )
    
        image_axes.set_axis_off()
        image_axes.imshow(grid, origin='upper', interpolation='nearest',
                          cmap=ct_cmap, norm=ct_norm)
    
        fig.savefig('imshow.png', dpi=dpi, facecolor=fig.get_facecolor(),
                    edgecolor='none', pad_inches=0.0)
        plt.close(fig)
    
        # Now the same grid with scipy imsave but also as an RGBA image.
    
        rgba = np.zeros((900, 600, 4))
        rgba[:, :, 0] = grid
        rgba[:, :, 1] = grid
        rgba[:, :, 2] = grid
        rgba[:, :, 3] = 255
        scipy.misc.imsave('scipyimsave.png', rgba)
    
    
    if __name__ == '__main__':
    
        make_image()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

---
title: min graph plotter
date: 2020-05-07
---
Example Python program min-graph-plotter.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import sys
* import matplotlib
* from mpl_toolkits.mplot3d import Axes3D
* import matplotlib.pyplot as plt
* import numpy as np
* import matplotlib.animation as manimation

## Methods

* def plotequ():

## Code

Python example

    import sys
    save_movie = False
    
    print('Usage for creating a video: python min-graph-plotter.py --movie')
    print('Usage for creating a pic  : python min-graph-plotter.py')
    
    def plotequ():
        import matplotlib
        if save_movie:
            matplotlib.use("Agg")
        from mpl_toolkits.mplot3d import Axes3D
        import matplotlib.pyplot as plt
        import numpy as np
        import matplotlib.animation as manimation
    
        if save_movie:
            FFMpegWriter = manimation.writers['ffmpeg']
            metadata = dict(title='Movie Test', artist='Matplotlib',
                            comment='Movie support!')
            writer = FFMpegWriter(fps=15, metadata=metadata)
    
        n_radii = 20
        n_angles = 36
    
        # Make radii and angles spaces (radius r=0 omitted to eliminate duplication).
        radii = np.linspace(0.125, 1.0, n_radii)
        angles = np.linspace(0, 2*np.pi, n_angles, endpoint=False)
    
        # Repeat all angles for each radius.
        angles = np.repeat(angles[..., np.newaxis], n_radii, axis=1)
    
        # Convert polar (radii, angles) coords to cartesian (x, y) coords.
        # (0, 0) is manually added at this stage,  so there will be no duplicate
        # points in the (x, y) plane.
        x = np.append(0, (radii*np.cos(angles)).flatten())
        y = np.append(0, (radii*np.sin(angles)).flatten())
    
        # Compute z to make the pringle surface.
        
        plt.rc('text', usetex=True)
        plt.rc('font', family='serif')
        fig = plt.figure(figsize=(12.4, 7.4), dpi=120)#fig size in inches
        ax = fig.gca(projection='3d')
        ax.set_facecolor('black')
    
        z = x*x + 2*x*y+ y*y #np.sin(-x*y)
        plt.title(r"$f(x, y) = x^2 + 2xy+ y^2$", color="#76DDC0", fontsize=26, fontweight='bold')
        # plt.title(r"\TeX\ is Number ", fontsize=16, color='#C9E2AE')
        # Make room for the large title.
        plt.subplots_adjust(top=0.8)
        plt.axis('off')
        ax.plot_trisurf(x, y, z, linewidth=0.01, antialiased=True, color = '#FF862F')
    
        # rotate the axes and update
        if save_movie:
            with writer.saving(fig, "writer_test.mp4", 100):
                for angle in range(0, 360, 1):
                    ax.view_init(30, angle)
                    plt.draw()
                    plt.rcParams['savefig.facecolor']='black'
                    plt.pause(.001)
                    writer.grab_frame()
        else:
            ax.view_init(30, 30)
            plt.draw()
            plt.rcParams['savefig.facecolor']='black'
    
        plt.show()
    
    if __name__ == "__main__":
        if '--movie' in sys.argv:
            save_movie = True
        else:
            save_movie = False
        plotequ()
        
    # Credits: 3Blue1Brown for color scheme

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

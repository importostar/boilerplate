---
title: animation
date: 2020-05-07
---
Example Python program animation.py

## Modules

* import math
* import numpy
* from scipy.stats import chi2
* from matplotlib import pyplot as plt
* from matplotlib import animation
* from matplotlib.patches import Ellipse

## Methods

* def cov_patch(centroid, cov, perc, alpha=0.5, color='b'):
* def scatter_animation():
* def animate(i):

## Code

Python example

    import math
    import numpy
    
    from scipy.stats import chi2
    from matplotlib import pyplot as plt
    from matplotlib import animation
    from matplotlib.patches import Ellipse
    
    
    def cov_patch(centroid, cov, perc, alpha=0.5, color='b'):
        """Example from matplotlib mailing list :
        http://www.mail-archive.com/matplotlib-users@lists.sourceforge.net/msg14153.html
        
        Combine with the computation of contours from :
        http://jtemplin.coe.uga.edu/files/multivariate/mv11icpsr/mv11icpsr_lecture04.pdf
        http://courses.education.illinois.edu/EdPsy584/lectures/MultivariateNormal-online.pdf
        """
        c = chi2.isf(1 - perc, 2)
        U, s, _ = numpy.linalg.svd(cov)
    
        width = 2.0 * math.sqrt(s[0] * c)
        height = 2.0 * math.sqrt(s[1] * c)
        orient = math.atan2(U[1][0], U[0][0]) * 180 / math.pi
    
        return Ellipse(xy=centroid, width=width, height=height, angle=orient, alpha=alpha, color=color, zorder=10)
    
    
    N_ITER = 50
    def scatter_animation():
        fig = plt.figure()
        ax = plt.subplot(111)
    
        # Create dummy data
        centroids = [numpy.zeros(2) + numpy.ones(2) * i for i in range(N_ITER)]
        covs = [numpy.eye(2) * 4] * N_ITER
        points_array = [numpy.random.multivariate_normal(centroids[i], covs[i], 100)
                        for i in range(N_ITER)]
    
        # Update plot limits based on the data
        x_min, y_min = numpy.min(numpy.min(points_array, axis=1), axis=0)
        x_max, y_max = numpy.max(numpy.max(points_array, axis=1), axis=0)
        ax.set_xlim(x_min, x_max)
        ax.set_ylim(y_min, y_max)
    
        # Initial scatter that will be modified
        points_scatter = ax.scatter(None, None, s=2, zorder=0)
    
        def animate(i):
            # Update scatter plot
            points_scatter.set_offsets(points_array[i])
    
            # Create new patches as they cannot be updated simply
            del ax.patches[:]
            ax.add_patch(cov_patch(centroids[i], covs[i], 0.8))
    
        anim = animation.FuncAnimation(fig, animate,
                                       frames=len(points_array),
                                       interval=100, # Time per frame in ms
                                       blit=False # Required with Mac OS X backend
                                       )
        anim.save("{prefix}.mp4".format(prefix="test"), dpi=90,
                  extra_args=['-vcodec', 'libx264', '-pix_fmt', 'yuv420p'])
    
        # To show the final result in loop
        plt.show()
    
    if __name__ == "__main__":
        scatter_animation()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

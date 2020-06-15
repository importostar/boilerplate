---
title: plot_focal_plane
date: 2020-05-07
---
Example Python program plot_focal_plane.py

## Modules

* import matplotlib.pyplot as plt
* from matplotlib.collections import PatchCollection
* from matplotlib.patches import Rectangle
* import lsst.afw.geom as afw_geom
* from lsst.afw import cameraGeom
* from lsst.obs.lsst.phosim import PhosimMapper

## Methods

* def get_amp_patches(det, amps=None):
* def plot_amp_boundaries(ax, camera=None, edgecolor='blue', facecolor='white'):

## Code

Python example

    import matplotlib.pyplot as plt
    from matplotlib.collections import PatchCollection
    from matplotlib.patches import Rectangle
    import lsst.afw.geom as afw_geom
    from lsst.afw import cameraGeom
    plt.ion()
    
    def get_amp_patches(det, amps=None):
        """
        Return a list of Rectangle patches in focalplane coordinates
        corresponding to the amplifier segments in a detector object.
        Parameters
        ----------
        det: `lsst.afw.cameraGeom.detector.detector.Detector`
            Detector object.
        amps: container-type object [None]
            Python container that can be queried like `'C01 in amps'`
            to see if a particular channel is included for plotting.
            If None, then use all channels in det.
        Returns
        -------
        list of matplotlib.patches.Rectangle objects
        """
        transform = det.getTransform(cameraGeom.PIXELS, cameraGeom.FOCAL_PLANE)
        bbox = det['C01'].getBBox()
        dy, dx = bbox.getHeight(), bbox.getWidth()
        patches = []
        for amp in det:
            if amps is not None and amp.getName() not in amps:
                continue
            j, i = tuple(int(_) for _ in amp.getName()[1:])
            y, x = j*dy, i*dx
            x0, y0 = transform.applyForward(afw_geom.Point2D(x, y))
            x1, y1 = transform.applyForward(afw_geom.Point2D(x + dx, y + dy))
            patches.append(Rectangle((x0, y0), x1 - x0, y1 - y0))
        return patches
    
    
    def plot_amp_boundaries(ax, camera=None, edgecolor='blue', facecolor='white'):
        """
        Plot the amplifier boundaries for all of the detectors in a camera.
        Parameters
        ----------
        ax: `matplotlib.Axes`
            Axes object used to render the patch collection containing
            the amplifier boundary Rectangles.
        camera: `lsst.afw.cameraGeom.camera.camera.Camera` [None]
            Camera object containing the detector info. If None, use
            `lsst.obs.lsst.imsim.ImsimMapper().camera`
        edgecolor: str or tuple of RGBA values ["blue"]
            Color used to draw outline of amplifiers.
        facecolor: str or tuple of RGBA values ["white"]
            Color used to render the Rectangle corresponding to the
            amplifier region.
        Returns
        -------
        None
        """
        if camera is None:
            camera = ImsimMapper().camera
        patches = []
        for det in camera:
            patches.extend(get_amp_patches(det))
        pc = PatchCollection(patches, edgecolor=edgecolor, facecolor=facecolor)
        ax.add_collection(pc)
    
    if __name__ == '__main__':
        from lsst.obs.lsst.phosim import PhosimMapper
    
        fig = plt.figure(figsize=(10, 10))
        ax = fig.add_subplot(1, 1, 1)
    
        camera = PhosimMapper().camera
        plot_amp_boundaries(ax, camera=camera)
        plt.xlim(-325, 325)
        plt.ylim(-325, 325)
        

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

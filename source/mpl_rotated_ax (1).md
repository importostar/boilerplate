---
title: mpl_rotated_ax (1)
date: 2020-05-07
---
Example Python program mpl_rotated_ax (1).py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import matplotlib.pyplot as plt
* import traceback
* from matplotlib.transforms import BboxTransformTo, TransformedBbox, Affine2D, Bbox, TransformWrapper
* import matplotlib.transforms as mtransforms
* from numpy import array
* from matplotlib.axes import Axes
* import numpy as np
* # The parentheses are important for efficiency here -- they

## Classes

* class MyAxes(Axes):
* class MyClass(object):

## Methods

* def label_set_rotation(label, offset=0.0):
* def __init__(self, *args, **kwargs):
* def rotate_deg_around_ax_center(self, angle):
* def patch(self, bboxes, bboxes2):
* def _set_lim_and_transforms(self):
* def xxx_apply_aspect(self, position=None):
* def xxx_get_position(self, original=False):
* def xxx_set_position(self, pos, which='both'):
* def bbox(self):
* def bbox(self, value):
* def _as_mpl_axes(self):

## Code

Python example

    import matplotlib.pyplot as plt
    import traceback
    
    fig = plt.figure()
    
    from matplotlib.transforms import BboxTransformTo, TransformedBbox, Affine2D, Bbox, TransformWrapper
    import matplotlib.transforms as mtransforms
    from numpy import array
    from matplotlib.axes import Axes
    
    import numpy as np
    
    def label_set_rotation(label, offset=0.0):
        # https://github.com/matplotlib/matplotlib/issues/698    
        label.set_rotation(offset +
            label.get_transform().transform_angles(
                np.array([0.0]),
                np.array([label.get_position()]))[0])
    
    
    class MyAxes(Axes):
        def __init__(self, *args, **kwargs):
            kwargs.pop('myclass', None)
    
            return Axes.__init__(self, *args, **kwargs)
    
    
        def rotate_deg_around_ax_center(self, angle):
            display_center = self.transAxes.transform((.5, .5))
            self.transAxes.set(
                Affine2D(
                    mtransforms.BboxTransformTo(self.bbox).get_matrix()
                ).rotate_deg_around(display_center[0], display_center[1], angle)
            )
    
    
            label_set_rotation(ax.title)
    
    
            # fudge the positioning of the labels
            self.xaxis.label.set_transform(self.transAxes)
            self.yaxis.label.set_transform(self.transAxes)
    
            self.xaxis.label.set_position((0.5, -0.03))
            self.yaxis.label.set_position((-0.03, 0.5))
            label_set_rotation(self.xaxis.label)
            label_set_rotation(self.yaxis.label, offset=90)
    
            # make sure label position doesn't get over-ridden
            def patch(self, bboxes, bboxes2):
                pass
    
            ax.xaxis._update_label_position = patch.__get__(ax.xaxis, ax.xaxis.__class__)
            ax.yaxis._update_label_position = patch.__get__(ax.yaxis, ax.yaxis.__class__)
    
    
        def _set_lim_and_transforms(self):
            self.transAxes = TransformWrapper(mtransforms.BboxTransformTo(self.bbox))
    
    
            # Transforms the x and y axis separately by a scale factor.
            # It is assumed that this part will have non-linear components
            # (e.g., for a log scale).
            self.transScale = mtransforms.TransformWrapper(
                mtransforms.IdentityTransform())
    
            # An affine transformation on the data, generally to limit the
            # range of the axes
            self.transLimits = mtransforms.BboxTransformFrom(
                mtransforms.TransformedBbox(self.viewLim, self.transScale))
    
            # The parentheses are important for efficiency here -- they
            # group the last two (which are usually affines) separately
            # from the first (which, with log-scaling can be non-affine).
            self.transData = self.transScale + (self.transLimits + self.transAxes)
    
            self.transDataToAxes = self.transScale + self.transLimits
    
            self._xaxis_transform = mtransforms.blended_transform_factory(
                self.transDataToAxes, mtransforms.IdentityTransform()) + self.transAxes
    
            self._yaxis_transform = mtransforms.blended_transform_factory(
                mtransforms.IdentityTransform(), self.transDataToAxes) + self.transAxes
            
        # for future development to see what relies on axis-aligned assumptions
        def xxx_apply_aspect(self, position=None):
            return
    
    
        def xxx_get_position(self, original=False):
            traceback.print_stack()
            #raise NotImplementedError()
    
    
        def xxx_set_position(self, pos, which='both'):
            traceback.print_stack()
            #raise NotImplementedError
    
        @property
        def bbox(self):
            #print("get bbox")
            #traceback.print_stack()
            return self._bbox
    
        @bbox.setter
        def bbox(self, value):
            #print("set bbox")
            #traceback.print_stack()        
            self._bbox = value
    
    
    class MyClass(object):
    
        def _as_mpl_axes(self):
            return MyAxes, {'myclass': self}
    
    ax = fig.add_subplot(1,1,1, projection=MyClass())
    
    xs = np.linspace(0,12) 
    l = ax.plot(xs, np.cos(xs))[0]
    l.set_clip_on(False)
    
    ax.set_xlabel("x axis")
    ax.set_ylabel("y axis")
    
    ax.set_title("Title")
    
    ax.rotate_deg_around_ax_center(15)

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

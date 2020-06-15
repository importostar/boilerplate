---
title: downsample patch
date: 2020-05-07
---
Example Python program downsample-patch.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* #   $ python -c "import matplotlib.lines as l; print(l.__file__)"
* #   import numpy as np; import matplotlib.pyplot as plt;

## Methods

* def _downsample_path(tpath, affine):
* def _slice_or_none(in_v, slc):
* def _draw_solid(self, renderer, gc, path, trans):
* def set_downsample(self, downsample):
* def get_downsample(self):

## Code

Python example

    
    # Add this to the bottom of lines.py inside matplotlib.
    # You can find the location of lines.py by running
    #   $ python -c "import matplotlib.lines as l; print(l.__file__)"
    #
    # Example installation:
    #   $ cp path/to/matplotlib/lines.py path/to/matplotlib/lines.py.old
    #   $ cat downsample-patch.py >> path/to/matplotlib/lines.py
    #
    # After it's installed, try the following:
    #   import numpy as np; import matplotlib.pyplot as plt;
    #   x = np.random.rand(1000000)
    #   plt.plot(x); plt.show() # slow!
    #   plt.plot(x, downsample=True); plt.show() # fast!
    
    def _downsample_path(tpath, affine):
        """    Helper function to compute the downsampled path.    """
        # pull out the two bits of data we want from the path
        codes, verts = tpath.codes, tpath.vertices
    
        def _slice_or_none(in_v, slc):
            """
            Helper function to cope with `codes` being an ndarray or `None`
            """
            if in_v is None:
                return None
            return in_v[slc]
    
        # Convert vertices from data space to pixel space.
        # Any non-affine axis transformation has already been applied
        # to tpath, so we just need to apply affine part.
        verts_trans = affine.transform_path(tpath).vertices
    
        # Find where the pixel column of the x data changes
        split_indices = np.diff(np.floor(verts_trans[:, 0]).astype(int)) != 0
        split_indices = np.where(split_indices)[0] + 1
    
        # Don't waste time downsampling if it won't give us any benefit
        # 4.0 was chosen somewhat arbitrarily.
        if split_indices.size >= verts_trans.shape[0] / 4.0:
            return tpath
    
        keep_inds = np.zeros((split_indices.size + 1, 4), dtype=int)
        for i, y_pixel_col in enumerate(np.split(verts_trans[:, 1],
                                                 split_indices)):
            try:
                keep_inds[i, 1:3] = (np.nanargmin(y_pixel_col),
                                     np.nanargmax(y_pixel_col))
            except ValueError:
                # np.nanarg* raises a ValueError if all elements are NaN.
                # If either np.nanargmin or np.nanargmax raise this error,
                # then all y_pixel_col is NaN. In this case, the argmin
                # and argmax are both undefined, just keep the first value.
                keep_inds[i, 1:3] = 0
    
        starts = np.hstack((0, split_indices))
        ends = np.hstack((split_indices, verts_trans.shape[0]))
        keep_inds[:, :3] += starts[:, np.newaxis]
        keep_inds[:, 3] = ends - 1
    
        keep_inds = keep_inds.flatten()
    
        return Path(verts[keep_inds], _slice_or_none(codes, keep_inds))
    
    _old_draw_solid = Line2D._draw_solid
    
    def _draw_solid(self, renderer, gc, path, trans):
        if getattr(self, "downsample", False):
            path = _downsample_path(path, trans)
        return _old_draw_solid(self, renderer, gc, path, trans)
    
    Line2D._draw_solid = _draw_solid
    
    # This stuff needed for python 2.7
    Line2D.downsample = False
    
    def set_downsample(self, downsample):
        self.downsample = downsample
        self.stale = True
    
    def get_downsample(self):
        return self.downsample
    
    Line2D.set_downsample = set_downsample
    Line2D.get_downsample = get_downsample

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

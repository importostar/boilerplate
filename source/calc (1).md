---
title: calc (1)
date: 2020-05-07
---
Example Python program calc (1).py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import numpy as np
* import matplotlib
* import matplotlib.pyplot as plt
* import matplotlib.patches as patches
* from matplotlib.path import Path
* from scipy.interpolate import interp2d

## Classes

* 	class DoInterp(object):

## Methods

* def interp_barycentric(x, y, fun):
* 		def __init__(self):
* 		def _lambdas(self, xv, yv):
* 		def __call__(self, xp, yp):
* 		def inside(self, xp, yp):
* def transform(x):
* def toUV(x):
* def toPath(vtx):

## Code

Python example

    #!/usr/bin/env python3
    
    import numpy as np
    import matplotlib
    matplotlib.use("Gtk3Cairo")
    import matplotlib.pyplot as plt
    import matplotlib.patches as patches
    from matplotlib.path import Path
    from scipy.interpolate import interp2d
    
    codes = [Path.MOVETO, Path.LINETO, Path.LINETO, Path.LINETO, Path.CLOSEPOLY,]
    
    def interp_barycentric(x, y, fun):
    	coord_matrix = np.row_stack([x, y, np.ones_like(x)])
    	bary_matrix = np.linalg.inv(coord_matrix)
    
    	class DoInterp(object):
    		def __init__(self):
    			pass
    
    		def _lambdas(self, xv, yv):
    			vec = np.row_stack([xv.reshape(-1), yv.reshape(-1), np.ones_like(xv.reshape(-1))])
    			return bary_matrix.dot(vec)
    
    		def __call__(self, xp, yp):
    			xv, yv = np.meshgrid(xp, yp)
    			lambdas = self._lambdas(xv, yv)
    			ret = np.zeros_like(xv)
    			ret = (fun.dot(lambdas).reshape(xv.shape))
    			return ret
    
    		def inside(self, xp, yp):
    			xv, yv = np.meshgrid(xp, yp)
    			lambdas = self._lambdas(xv, yv)
    			inside = np.logical_not(np.apply_along_axis(lambda x: (x < 0).any(), 0, lambdas))
    			ret = np.zeros_like(xv, dtype=bool)
    			ret = inside.reshape(xv.shape)
    			return ret
    
    	return DoInterp()
    
    def transform(x):
    	X = x[:,0]
    	Y = x[:,1]
    	return np.column_stack([-0.5+2.0*(X+0.5*Y**2),-0.5+2.0*(Y+0.5*X**2)])
    
    def toUV(x):
    	X = x[:,0]
    	Y = x[:,1]
    	return np.column_stack([X + 0.5, Y + 0.5])
    
    def toPath(vtx):
    	verts = [tuple(v) for v in vtx] + [(0.0,0.0),]
    	path = Path(verts, codes)
    	return path
    
    vtx = np.array([
    	[-1,-1],
    	[-1,1],
    	[1,1],
    	[1,-1],
    ], dtype=float)
    
    UV = vtx + 0.5
    
    # 0 2 1 3
    
    vtx2 = transform(vtx)
    
    interp_x = interp2d(vtx2[:,0], vtx2[:,1], vtx[:,0])
    interp_y = interp2d(vtx2[:,0], vtx2[:,1], vtx[:,1])
    
    vtx_UV = np.array([-0.5,0.5])
    
    sink_UV = np.zeros(shape=(vtx_UV.shape[0], vtx_UV.shape[0], 2))
    for tri in [[0,1,2],[0,2,3]]:
    	itrp_x = interp_barycentric(vtx2[tri,0], vtx2[tri,1], UV[tri,0])
    	itrp_y = interp_barycentric(vtx2[tri,0], vtx2[tri,1], UV[tri,1])
    	UVp_x = itrp_x(vtx_UV, vtx_UV)
    	UVp_y = itrp_y(vtx_UV, vtx_UV)
    	inside = itrp_x.inside(vtx_UV, vtx_UV)
    	UVp = np.column_stack([UVp_x.flatten(),UVp_y.flatten()])
    	sink_UV[inside, 0] = UVp_x[inside]
    	sink_UV[inside, 1] = UVp_y[inside]
    
    print(sink_UV)
    
    path_UV = toPath(vtx / 2)
    path_2 = toPath(vtx2)
    path = toPath(vtx)
    
    fig = plt.figure()
    ax = fig.add_subplot(111)
    patch_2 = patches.PathPatch(path_2, lw=1, facecolor='None')
    patch_UV = patches.PathPatch(path_UV, lw=1, facecolor='None', ls="--")
    patch = patches.PathPatch(path, lw=1, facecolor='None')
    ax.add_patch(patch_2)
    ax.add_patch(patch_UV)
    ax.add_patch(patch)
    ax.set_xlim(-6,6)
    ax.set_ylim(-6,6)
    plt.show()
    
    
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

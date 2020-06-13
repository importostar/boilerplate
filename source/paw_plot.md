---
title: paw_plot
date: 2020-05-07
---
Example Python program paw_plot.py

## Modules

* import matplotlib.pyplot as plt
* import numpy as np
* import matplotlib.patches as mpatch
* from matplotlib.collections import PatchCollection
* import matplotlib.colors as mcolors
* import matplotlib.colorbar 
* import matplotlib.gridspec as gridspec

## Methods

* def mega_paw_plot(sdata_list=None, sdata_bg_list=None, cdata_list=None, 
* def paw_plot(sdata=None, sdata_bg=None, cdata=None, cmap=None, clim=None, edgecolor='#555555', bgcolor='#cccccc', legend=True, ax=None):

## Code

Python example

    import matplotlib.pyplot as plt
    import numpy as np
    import matplotlib.patches as mpatch
    from matplotlib.collections import PatchCollection
    import matplotlib.colors as mcolors
    import matplotlib.colorbar 
    import matplotlib.gridspec as gridspec
    
    def mega_paw_plot(sdata_list=None, sdata_bg_list=None, cdata_list=None, 
                      cmap=None, clim=None, 
                      edgecolor='#555555', bgcolor='#cccccc', 
                      figsize=None, cbar_orientation='horizontal'):
        if cmap is None:
            cmap = 'magma'
            
        lens = []
        for dl in [ sdata_list, sdata_bg_list, cdata_list ]:
            if dl is not None:
                lens.append(len(dl))
        
        if len(np.unique(lens)) != 1:
            raise Exception("sdata_list, sdata_bg_list, and cdata_list must have the same length")
            
        nrows = len(sdata_list)
        fig = plt.figure(figsize=figsize)
        if cbar_orientation == 'vertical':
            gs = gridspec.GridSpec(nrows, 2, width_ratios=[10, 1])
        elif cbar_orientation == 'horizontal':
            gs = gridspec.GridSpec(nrows+1, 1, height_ratios=[10]*nrows + [1])
        
        for i, (sdata, sdata_bg, cdata) in enumerate(zip(sdata_list, sdata_bg_list, cdata_list)):
            ax = plt.subplot(gs[i,0])
            paw_plot(sdata, sdata_bg, cdata, cmap, clim, edgecolor, bgcolor, legend=False, ax=ax)
                
        if cdata_list:
            if cbar_orientation == 'vertical':
                cbar_ax = plt.subplot(gs[:,1])
            elif cbar_orientation == 'horizontal':
                cbar_ax = plt.subplot(gs[-1])
                
            if clim:
                norm = mcolors.Normalize(vmin=clim[0], vmax=clim[1])
            else:
                norm = mcolors.Normalize(vmin=min([cdata.min() for cdata in cdata_list]),
                                         vmax=max([cdata.max() for cdata in cdata_list]))
            cbar = matplotlib.colorbar.ColorbarBase(cbar_ax, cmap=cmap,
                                                    norm=norm,
                                                    orientation=cbar_orientation)
    
        
    def paw_plot(sdata=None, sdata_bg=None, cdata=None, cmap=None, clim=None, edgecolor='#555555', bgcolor='#cccccc', legend=True, ax=None):
        ax = ax if ax else plt.gca()
            
        r = np.array([ 0, 1, 1, 1, 1, 1 ])
        theta = np.array([ 0, 30, 72, 114, 156, 198 ]) * np.pi / 180.0
        
        if sdata is None:
            sdata = np.array([4,1,1,1,1,1])*.08
                    
        if cdata is None:
            cdata = np.ones(len(r))
        
        if cmap is None:
            cmap = 'magma'
            
        if clim is None:
            clim = [0,1]
        
        xx = r * np.cos(theta)
        yy = r * np.sin(theta)            
        
        patches = [ mpatch.Circle((x,y),rad) for (x,y,rad) in zip(xx,yy,np.sqrt(sdata)) ]
        col = PatchCollection(patches, zorder=2)
        col.set_array(cdata)    
        col.set_cmap(cmap)
        col.set_edgecolor(edgecolor)
        col.set_clim(vmin=clim[0], vmax=clim[1])        
        
        ax.add_patch(mpatch.Arc((0.0, 0.0), 2.0, 2.0, angle=0.0, 
                                theta1=theta[1]*180.0/np.pi, theta2=theta[-1]*180.0/np.pi, 
                                edgecolor=edgecolor,facecolor='none', zorder=0, linestyle='--'))
       
        ax.add_collection(col)
        
        
        if legend:
            plt.colorbar(col)
            
        if sdata_bg is not None: 
            patches = [ mpatch.Circle((x,y),rad) for (x,y,rad) in zip(xx,yy,np.sqrt(sdata_bg)) ]
            col = PatchCollection(patches, zorder=1)
            col.set_edgecolor(edgecolor)
            col.set_facecolor(bgcolor)
            ax.add_collection(col)   
        
        ax.axis('equal')   
        ax.axis('off')
        
        ax.set_xlim([-1.2,1.2])
        ax.set_ylim([-.8,1.35])
    
    if __name__ == "__main__":
        mega_paw_plot(sdata_list=[ np.array([5,1,1,1,1,1])*.05, np.array([5,2,1,1,1,1])*.05, np.array([2,1,.5,.5,.5])*.0005 ],
                      sdata_bg_list=[ np.array([7,2.5,2,2,2,2])*.05, np.array([6,2.5,2,2,2,2])*0.05, np.array([2.1,2.5,2,2,2,2])*.0005 ],
                      cdata_list=[ np.random.random(6), np.random.random(6)*3, np.random.random(6)*2 ],
                      cmap='hot',
                      clim=[0.0,5.0],
                      figsize=(5,15),
                      cbar_orientation='horizontal')
        plt.show()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

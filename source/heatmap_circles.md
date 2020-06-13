---
title: heatmap_circles
date: 2020-05-07
---
Example Python program heatmap_circles.py

## Modules

* import numpy as np
* import matplotlib.pyplot as plt
* import matplotlib as mpl
* from matplotlib.collections import PatchCollection

## Methods

* def heatmap_circle(input_colors, input_sizes, 

## Code

Python example

    import numpy as np
    import matplotlib.pyplot as plt
    import matplotlib as mpl
    from matplotlib.collections import PatchCollection
    
    #### heatmap_circle()
    ##
    ## Creates a heatmap of values, with size of the circle at a given (row,col) as a second dimension
    ## uses seaborn's clustermap to provide biclustering
    ##
    ## -Ryan Neff, 2020.
    ##
    #### Inputs
    #
    # input_colors: pd.DataFrame of numeric types without None / nan, required
    #     These are the values you wish to be plotted as colors on the heatmap. They will be scaled.
    #
    # input_sizes: pd.DataFrame of numeric types without None / nan, required
    #     These are the values you wish to be the sizes of the circles. They will be scaled. 0 is allowed.
    #
    # row_cluster, col_cluster: boolean, optional
    #     Should we cluster the rows and/or columns using seaborn's clustermap? T/F
    #
    # cluster_on: String of ("color", "size", "none"), optional
    #     Which values should we cluster on? Only takes effect if row or column clustering is True. 
    #     "none" will disable clustering.
    #
    # method: String, optional
    #     Linkage method to use for calculating clusters. See scipy.cluster.hierarchy.linkage 
    #     documentation for more information: https://docs.scipy.org/doc/scipy/reference/generated/scipy.cluster.hierarchy.linkage.html
    #
    # vmin, vmax = numeric or None, optional
    #     For scaling the heatmap colors within a certain minimum and maximum range.
    #     See https://matplotlib.org/3.1.3/api/_as_gen/matplotlib.colors.Normalize.html. 
    #
    # cmap = String or a matplotlib.colors colormap object, optional
    #   Matplotlib colormap to use. See https://matplotlib.org/3.1.0/tutorials/colors/colormaps.html. 
    #
    #### Outputs
    #
    # A matplotlib figure representing the heatmap.
    #
    ######
    
    def heatmap_circle(input_colors, input_sizes, 
                       row_cluster=True, col_cluster=True, 
                       cluster_on="color", method="ward", vmin=None, vmax=None,
                       cmap="RdBu_r"): #color = DEG, size = significance p-value
    
        if input_colors.shape != input_sizes.shape:
            raise InputError("Input matrices must be the same shape.")
        if all(input_colors.index == input_sizes.index) == False:
            raise InputError("Input indexes and order must be equal.")
        if all(input_colors.columns == input_sizes.columns) == False:
            raise InputError("Input columns and order must be equal.")
        
        
        if cluster_on=="color":
            clustergrid = sb.clustermap(input_colors,cmap="RdBu_r",
                                        row_cluster=row_cluster,col_cluster=col_cluster, method=method)
            row_order = clustergrid.dendrogram_row.reordered_ind if row_cluster else range(len(input_colors.index))
            col_order = clustergrid.dendrogram_col.reordered_ind if col_cluster else range(len(input_colors.columns))
            input_colors = input_colors.iloc[row_order,col_order]
            input_sizes = input_sizes.iloc[row_order,col_order]
            plt.clf()
        elif cluster_on=="size":
            clustergrid = sb.clustermap(input_sizes,cmap="RdBu_r",
                                        row_cluster=row_cluster,col_cluster=col_cluster, method=method)
            row_order = clustergrid.dendrogram_row.reordered_ind if row_cluster else range(len(input_colors.index))
            col_order = clustergrid.dendrogram_col.reordered_ind if col_cluster else range(len(input_colors.columns))
            input_colors = input_colors.iloc[row_order,col_order]
            input_sizes = input_sizes.iloc[row_order,col_order]
            plt.clf()
            
        fig, ax = plt.subplots()
    
        N,M = input_colors.shape
        ylabels = list(input_colors.index)
        xlabels = list(input_colors.columns)
    
        x, y = np.meshgrid(np.arange(M), np.arange(N))
        s = input_sizes.values #size column
        c = input_colors.values
    
        R = s/s.max()/2
        circles = [plt.Circle((j,i), radius=r) for r, j, i in zip(R.flat, x.flat, y.flat)]
        col = PatchCollection(circles, array=c.flatten(), cmap=cmap,norm=mpl.colors.Normalize(vmin=vmin,vmax=vmax))
        ax.add_collection(col)
    
        ax.set(xticks=np.arange(M), yticks=np.arange(N),
               xticklabels=xlabels, yticklabels=ylabels)
        ax.set_xticks(np.arange(M+1)-0.5, minor=True)
        ax.set_yticks(np.arange(N+1)-0.5, minor=True)
        #ax.grid(which='minor')
    
        ax.set_facecolor((1,1,1,0))
        plt.grid(b=None)
        fig.colorbar(col)
        plt.gca().set_aspect('equal', adjustable='box')
        plt.setp(ax.get_xticklabels(), rotation=90,ha="right")

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

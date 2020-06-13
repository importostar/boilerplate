---
title: plotter (1)
date: 2020-05-07
---
Example Python program plotter (1).py

## Modules

* import matplotlib.pyplot as plt
* import matplotlib
* from matplotlib import ticker
* from mpl_toolkits.basemap import Basemap

## Methods

* def _plot_2d_map_with_averages(data, lons, lats, vminn, vmaxx, figfilename=None, cmap=plt.get_cmap('rainbow'), barmin=None, barmax=None, figtitle=None):

## Code

Python example

    def _plot_2d_map_with_averages(data, lons, lats, vminn, vmaxx, figfilename=None, cmap=plt.get_cmap('rainbow'), barmin=None, barmax=None, figtitle=None):
        import matplotlib.pyplot as plt
        import matplotlib
        from matplotlib import ticker
        from mpl_toolkits.basemap import Basemap
        fig = plt.figure(figsize=(14,8))
        ax1 = plt.subplot2grid((3, 5), (0, 0), colspan=4, rowspan=2)
        ax2 = plt.subplot2grid((3, 5), (0, 4), rowspan=2, sharey=ax1)
        ax3 = plt.subplot2grid((3, 5), (2, 0), colspan=4, sharex=ax1)
    
        b = Basemap(projection='cyl',ax=ax1)
        b.drawcoastlines()
        map_lons, map_lats = np.meshgrid(lons, lats)
        map_lons, map_lats = b(map_lons, map_lats)
    
        b.pcolor(map_lons, map_lats, data, vmin=vminn, vmax=vmaxx, cmap=cmap)
        ax1.set_xticks([])
        ax1.set_yticks([])
        if figtitle is not None:
            ax1.set_title(figtitle, fontsize=16)
    
        ax2.plot( np.nanmean(data, axis=1), [x for x in lats[:-1]] )
        ax2.set_ylim([-90,90])
        ax2.set_yticks([x for x in np.arange(-90,90.01,30)])
        ax2.set_yticklabels([str(x) for x in np.arange(-90,90.01,30)])
        ax2.set_ylabel('Latitude',fontsize=16)
        ax2.tick_params(axis='both', which='major', labelsize=14)
        ax2.yaxis.tick_right()
        ax2.yaxis.set_label_position('right')
        if barmin is not None and barmax is not None:
            ax2.set_xlim([barmin, barmax])
    
        ax3.plot( [x for x in lons[:-1]], np.nanmean(data, axis=0) )
        ax3.set_xlim([-180,180])
        ax3.set_xticks([x for x in np.arange(-180.0,180.01,30)])
        ax3.set_xticklabels([str(x) for x in np.arange(-180,180.01,30)])
        ax3.set_xlabel('Longitude',fontsize=16)
        ax3.tick_params(axis='both', which='major', labelsize=14)
        if barmin is not None and barmax is not None:
             ax3.set_ylim([barmin, barmax])
    
        fig.subplots_adjust(hspace=0, wspace=0)
        plt.setp(ax1.get_xticklabels(), visible=False)
        plt.setp(ax1.get_yticklabels(), visible=False)
    
        ax4 = fig.add_axes([0.77, 0.225, 0.17, 0.05])
        norm = matplotlib.colors.Normalize(vmin=vminn, vmax=vmaxx)
        tick_locator = ticker.MaxNLocator(nbins=5)
        cb = matplotlib.colorbar.ColorbarBase(ax4, orientation='horizontal', norm=norm, cmap=cmap)
        cb.ax.tick_params(labelsize=16)
        cb.locator = tick_locator
        cb.update_ticks()
    
        if figfilename is not None:
            plt.savefig(figfilename)
            plt.close()
        else:
            plt.show()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

---
title: convert_ParaView_xml_to_matplotlib_colormap
date: 2020-05-07
---
Example Python program convert_ParaView_xml_to_matplotlib_colormap.py

## Modules

* from lxml import etree
* import os
* from matplotlib.colors import LinearSegmentedColormap
* import numpy as np
* import matplotlib.pyplot as plt
* from numpy.random import randn
* from optparse import OptionParser

## Methods

* def convert_ParaView_xml_to_matplotlib_colormap(fname='FloatPNG_PV44.xml'):
* def noise_example_colorbar(listcm):

## Code

Python example

    #!/usr/bin/env python
    # Phillip Wolfram
    # 07/01/2015
    
    from lxml import etree
    import os
    from matplotlib.colors import LinearSegmentedColormap
    
    
    def convert_ParaView_xml_to_matplotlib_colormap(fname='FloatPNG_PV44.xml'):
        """ Simple script that converts ParaView xml file into matplotlib cmap data structure.
        This can be tested at teh command line via
        python convert_ParaView_xml_to_matplotlib_colormap.py -f test.xml
        Phillip Wolfram
        07/01/2015
        """
    
        xmlfile = etree.parse(fname)
        root = xmlfile.getroot()
    
        x = []
        r = []
        g = []
        b = []
        for colormap in root.findall('ColorMap'):
            for point in colormap.findall('Point'):
                x.append(float(point.get('x')))
                r.append(float(point.get('r')))
                g.append(float(point.get('g')))
                b.append(float(point.get('b')))
    
        # now we have all the data in lists and we can build up the colormap
        cmdata = dict()
        cmdata['red'] = []
        cmdata['green'] = []
        cmdata['blue'] = []
        for xi,ri,gi,bi in zip(x,r,g,b):
            cmdata['red'].append((xi, ri, ri))
            cmdata['green'].append((xi, gi, gi))
            cmdata['blue'].append((xi, bi, bi))
        cmdata['red'] = tuple(cmdata['red'])
        cmdata['green'] = tuple(cmdata['green'])
        cmdata['blue'] = tuple(cmdata['blue'])
        cmapname = os.path.splitext(fname)[0]
        cm = LinearSegmentedColormap(cmapname, cmdata)
    
        return cm
    
    def noise_example_colorbar(listcm):
        """ example adapted from http://matplotlib.org/examples/pylab_examples/colorbar_tick_labelling_demo.html """
        import numpy as np
        import matplotlib.pyplot as plt
        from numpy.random import randn
    
        data = np.clip(randn(250, 250), -1, 1)
    
        for idx, cm in enumerate(listcm):
            # Make plot with vertical (default) colorbar
            fig, ax = plt.subplots()
    
            cax = ax.imshow(data, interpolation='nearest', cmap=cm)
            ax.set_title('Gaussian noise with vertical colorbar')
    
            # Add colorbar, make sure to specify tick locations to match desired ticklabels
            cbar = fig.colorbar(cax, ticks=[-1, 0, 1])
            cbar.ax.set_yticklabels(['< -1', '0', '> 1'])# vertically oriented colorbar
    
            # Make plot with horizontal colorbar
            fig, ax = plt.subplots()
    
            cax = ax.imshow(data, interpolation='nearest', cmap=cm)
            ax.set_title('Gaussian noise with horizontal colorbar')
    
            cbar = fig.colorbar(cax, ticks=[-1, 0, 1], orientation='horizontal')
            cbar.ax.set_xticklabels(['Low', 'Medium', 'High'])# horizontal colorbar
    
            plt.savefig('cm' + str(idx) + '.png')
    
    if __name__ == "__main__":
        from optparse import OptionParser
    
        # get command line parameters
        parser = OptionParser()
        parser.add_option("-f", "--file", dest="fname",
                help="xml file name for conversion to matplotlib colormap",
                metavar="FILE")
    
        options, args  = parser.parse_args()
    
        if not options.fname:
            parser.error("Filename is required input")
    
        fname = options.fname
    
        cm = convert_ParaView_xml_to_matplotlib_colormap(fname)
        noise_example_colorbar(cm)
        print cm
    
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

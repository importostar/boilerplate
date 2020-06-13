---
title: venn3_demo_for_Jupyter_notebook_cell (1)
date: 2020-05-07
---
Example Python program venn3_demo_for_Jupyter_notebook_cell (1).py

## Modules

* from matplotlib import pyplot as plt
* from matplotlib_venn import venn3, venn3_circles

## Code

Python example

    %matplotlib notebook
    from matplotlib import pyplot as plt
    from matplotlib_venn import venn3, venn3_circles
    #**REQUIRES `matplotlib_venn` ADDED TO `REQUIREMENTS.TXT` FOR BINDER, or run `%pip install matplotlib_venn` first**
    #**One already set like that can be launched from https://github.com/fomightez/vpython-jupyter ***
    # NOTE: I corrected the Subset labels according to info I posted at
    # http://matthiaseisen.com/pp/patterns/p0145/ , which is
    # where this code was adapted from
    
    # Subset sizes
    s = (
        2,    # Abc
        3,    # aBc
        4,    # ABc
        3,    # abC
        1,    # AbC
        0.5,  # aBC
        4,    # ABC
    )
    
    v = venn3(subsets=s, set_labels=('A', 'B', 'C'))
    
    # Subset labels
    v.get_label_by_id('100').set_text('Abc')
    v.get_label_by_id('010').set_text('aBc')
    v.get_label_by_id('110').set_text('ABc')
    v.get_label_by_id('001').set_text('abC')
    v.get_label_by_id('101').set_text('AbC')
    v.get_label_by_id('011').set_text('aBC')
    v.get_label_by_id('111').set_text('ABC')
    
    # Subset colors
    v.get_patch_by_id('100').set_color('c')
    v.get_patch_by_id('010').set_color('#993333')
    v.get_patch_by_id('110').set_color('blue')
    
    # Subset alphas
    v.get_patch_by_id('101').set_alpha(0.4)
    v.get_patch_by_id('011').set_alpha(1.0)
    v.get_patch_by_id('111').set_alpha(0.7)
    
    # Border styles
    c = venn3_circles(subsets=s, linestyle='solid')
    c[0].set_ls('dotted')  # Line style
    c[1].set_ls('dashed')
    c[2].set_lw(1.0)       # Line width
    
    plt.show()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

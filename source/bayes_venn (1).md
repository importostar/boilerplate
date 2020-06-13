---
title: bayes_venn (1)
date: 2020-05-07
---
Example Python program bayes_venn (1).py

## Modules

* import matplotlib
* from collections import Counter
* from matplotlib import pyplot as plt
* from matplotlib import patches as mpatches
* from matplotlib.lines import Line2D
* from matplotlib_venn import venn2

## Classes

* class bayes_venn_plotter:

## Methods

* def __init__(self, fname):
* def __enter__(self):
* def config(self, ap, bp, allp):
* def __exit__(self, exception_type, exception_value, traceback):

## Code

Python example

    import matplotlib
    matplotlib.use('AGG')
    
    from collections import Counter
    from matplotlib import pyplot as plt
    from matplotlib import patches as mpatches
    from matplotlib.lines import Line2D
    from matplotlib_venn import venn2
    
    
    class bayes_venn_plotter:
    
        def __init__(self, fname):
            self.fname = fname
    
        def __enter__(self):
            return self
    
        def config(self, ap, bp, allp):
            bgc = 'skyblue'
            plt.figure()
            plt.rc('text', aa=True, usetex=True)
            plt.title('Venn Diagram')
    
            sets = Counter()
            sets['01'] = bp
            sets['11'] = allp
            sets['10'] = ap
            setLabels = [r'event $A$', r'event $B$']
    
            ax = plt.gca()
            ax.text(0.02, 0.95, r'$\Omega$', transform=ax.transAxes)
            v = venn2(subsets=sets, set_labels=setLabels, ax=ax, alpha=0.6)
            st = [r"$A\cap B$", "", ""]
            h, l = [], []
    
            for ind, i in enumerate(sets):
                v.get_label_by_id(i).set_text(st[ind])
                h.append(v.get_patch_by_id(i))
                l.append(sets[i])
    
            h.append(mpatches.Patch(color=bgc))
            l.append(200)
            self.lgd = ax.legend(
                handles=h,
                labels=l,
                title="counts",
                loc=9,
                ncol=len(l),
                bbox_to_anchor=(0.5, -0.05),
                shadow=True)
            ax.set_facecolor(bgc)
            ax.set_axis_on()
    
        def __exit__(self, exception_type, exception_value, traceback):
            plt.savefig(
                self.fname,
                additional_artists=[self.lgd],
                bbox_inches="tight",
                antialiased=True)
    
    
    if __name__ == '__main__':
        with bayes_venn_plotter('bayes_venn.png') as p:
            p.config(60, 40, 10)
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

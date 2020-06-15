---
title: errormsg (1)
date: 2020-05-07
---
Example Python program errormsg (1).py


## Code

Python example

    Traceback (most recent call last):
      File "<input>", line 1, in <module>
      File "/Users/john/.conda/envs/mneredux/lib/python3.7/site-packages/mne/preprocessing/ica.py", line 1633, in plot_properties
        figsize=figsize, show=show, reject=reject)
      File "/Users/john/.conda/envs/mneredux/lib/python3.7/site-packages/mne/viz/ica.py", line 472, in plot_ica_properties
        plt_show(show)
      File "/Users/john/.conda/envs/mneredux/lib/python3.7/site-packages/mne/viz/utils.py", line 110, in plt_show
        (fig or plt).show(**kwargs)
      File "/Users/john/.conda/envs/mneredux/lib/python3.7/site-packages/matplotlib/pyplot.py", line 272, in show
        return _show(*args, **kw)
      File "/Applications/PyCharm with Anaconda plugin .app/Contents/plugins/python/helpers/pycharm_matplotlib_backend/backend_interagg.py", line 27, in __call__
        manager.show(**kwargs)
      File "/Applications/PyCharm with Anaconda plugin .app/Contents/plugins/python/helpers/pycharm_matplotlib_backend/backend_interagg.py", line 99, in show
        self.canvas.show()
      File "/Applications/PyCharm with Anaconda plugin .app/Contents/plugins/python/helpers/pycharm_matplotlib_backend/backend_interagg.py", line 64, in show
        self.figure.tight_layout()
      File "/Users/john/.conda/envs/mneredux/lib/python3.7/site-packages/matplotlib/cbook/deprecation.py", line 358, in wrapper
        return func(*args, **kwargs)
      File "/Users/john/.conda/envs/mneredux/lib/python3.7/site-packages/matplotlib/figure.py", line 2482, in tight_layout
        subplotspec_list = get_subplotspec_list(self.axes)
      File "/Users/john/.conda/envs/mneredux/lib/python3.7/site-packages/matplotlib/tight_layout.py", line 249, in get_subplotspec_list
        subplotspec = subplotspec.get_topmost_subplotspec()
    AttributeError: 'NoneType' object has no attribute 'get_topmost_subplotspec'
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

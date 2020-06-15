---
title: plot_with_chinese
date: 2020-05-07
---
Example Python program plot_with_chinese.py
For Python version 2.x.
To test your Python version use:

    python --version

## Modules

* from matplotlib import pyplot as plt
* import matplotlib
* from matplotlib.font_manager import *  
* from pylab import mpl
* import seaborn as sns

## Methods

* def get_matplot_zh_font():
* def set_matplot_zh_font():

## Code

Python example

    from matplotlib import pyplot as plt
    import matplotlib
    from matplotlib.font_manager import *  
    from pylab import mpl
    
    import seaborn as sns
    %matplotlib inline
    def get_matplot_zh_font():
        fm = FontManager()
        mat_fonts = set(f.name for f in fm.ttflist)
    
        output = subprocess.check_output('fc-list :lang=zh -f "%{family}\n"', shell=True)
        zh_fonts = set(f.split(',', 1)[0] for f in output.split('\n'))
        available = list(mat_fonts & zh_fonts)
    
        print '*' * 10, '可用的字体', '*' * 10
        for f in available:
            print f
        return available
    def set_matplot_zh_font():
        available = get_matplot_zh_font()
        if len(available) > 0:
            mpl.rcParams['font.sans-serif'] = [available[0]]    # 指定默认字体
            mpl.rcParams['axes.unicode_minus'] = False          # 解决保存图像是负号'-'显示为方块的问题
    set_matplot_zh_font()       

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

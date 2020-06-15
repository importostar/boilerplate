---
title: use_custom_font (1)
date: 2020-05-07
---
Example Python program use_custom_font (1).py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import matplotlib as mpl
* import matplotlib.pyplot as plt
* import matplotlib.font_manager as font_manager

## Code

Python example

    # 1. before use this script, you need to get a customed ttf font file, maybe you have only ttc file ,you can convert it to ttf in
    # this awesome web: http://www.zhuan-huan.com/file-convert/
    # 2. then edit the matplotlibrc file(for env most in envs/py3/lib/python3.5/site-packages/matplotlib/mpl-data ), uncomment two lines:
    #    font.family          : sans-serif
    #    font.sans-serif      :WenQuanYi Zen Hei,Bitstream Vera Sans, Lucida Grande, Verdana, Geneva, Lucid...
    # if your ttf font is sans-serif,you need only to add your new font name to the head of font.sans-serif.
    
    import matplotlib as mpl
    import matplotlib.pyplot as plt
    import matplotlib.font_manager as font_manager
    
    path = '/home/june/anaconda2/envs/py3/lib/python3.5/site-packages/matplotlib/mpl-data/fonts/ttf/wqy_zenhei.ttf'
    prop = font_manager.FontProperties(fname=path)
    print(prop.get_family())
    print(prop.get_name())
    
    # if you want to dynamic change font in code, you can step over step 2 above and copy fellow lines code to your work.
    mpl.rcParams['font.family'] = prop.get_name()
    
    # here is example.
    fig, ax = plt.subplots()
    ax.set_title('中国是个美丽的国家', size=40)
    plt.show()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

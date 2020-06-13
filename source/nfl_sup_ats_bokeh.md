---
title: nfl_sup_ats_bokeh
date: 2020-05-07
---
Example Python program nfl_sup_ats_bokeh.py
For Python version 2.x.
To test your Python version use:

    python --version

## Modules

* import csv, os
* import numpy as np
* import pandas as pd
* from datetime import datetime
* import matplotlib.pyplot as plt
* import matplotlib
* from math import pi
* from bokeh.plotting import figure, output_file, output_notebook, show, ColumnDataSource
* from bokeh.models import HoverTool, Legend, Circle, Square

## Code

Python example

    import csv, os
    import numpy as np
    import pandas as pd
    # print pd.__version__
    
    from datetime import datetime
    
    import matplotlib.pyplot as plt
    import matplotlib
    matplotlib.style.use('ggplot')
    %matplotlib inline
    
    home_lines = pd.read_csv('data/ATS_SUP_home_conf.csv', sep=';')
    print home_lines.shape
    print home_lines.dtypes
    print ''
    print home_lines.head()    # only first 3 weeks of season at this point
    
    # (48, 9)
    # week                object
    # away_short_name     object
    # home_short_name     object
    # away_score           int64
    # home_score           int64
    # home_line          float64
    # home_conf           object
    # home_favBy         float64
    # home_ptd             int64
    # dtype: object
    
    #      week away_short_name home_short_name  away_score  home_score  home_line  \
    # 0  Week 1             CAR             DEN          20          21        3.5   
    # 1  Week 1             BUF             BAL           7          13       -3.5   
    # 2  Week 1             CHI             HOU          14          23       -6.5   
    # 3  Week 1             CIN             NYJ          23          22        2.5   
    # 4  Week 1             CLE             PHI          10          29       -3.5   
    
    #   home_conf  home_favBy  home_ptd  
    # 0       AFC        -3.5         1  
    # 1       AFC         3.5         6  
    # 2       AFC         6.5         9  
    # 3       AFC        -2.5        -1  
    # 4       NFC         3.5        19 
    
    home_lines['ats_ptd'] = home_lines.home_ptd - home_lines.home_favBy
    home_lines['abs_line_ptd'] = np.absolute(home_lines.home_favBy - home_lines.home_ptd)
    # not a perfect way of making smaller points visible // get over it
    home_lines['marker_size'] = home_lines.abs_line_ptd + 2.0/home_lines.abs_line_ptd
    
    
    ### now, the plot
    
    from math import pi
    from bokeh.plotting import figure, output_file, output_notebook, show, ColumnDataSource
    from bokeh.models import HoverTool, Legend, Circle, Square
    
    output_notebook()
    
    output_file("sup_ats.html")
    
    bk_afc = home_lines[home_lines.home_conf=='AFC']
    bk_nfc = home_lines[home_lines.home_conf=='NFC']
    
    source_afc = ColumnDataSource(data=bk_afc)
    source_nfc = ColumnDataSource(data=bk_nfc)
    
    TOOLS = "pan,wheel_zoom,reset,save"
    
    p = figure(plot_width=600, plot_height=600, tools=TOOLS,
               title="2016 Performance SUP & ATS (through week 3)"
              )
    
    # http://stackoverflow.com/questions/29435200/bokeh-plotting-enable-tooltips-for-only-some-glyphs
    g1 = Circle(x='home_favBy', y='home_ptd', 
                size='marker_size', fill_color="firebrick",
                line_width=0.5,
                fill_alpha=0.5)
    g1_r = p.add_glyph(source_or_glyph=source_afc, glyph=g1)
    g1_hover = HoverTool(renderers=[g1_r],
                             tooltips=[("Game", "@away_short_name at @home_short_name"),
                                       ("Final Score", "@away_score - @home_score"),
                                       ("Home Line", "@home_line"),
                                       ("Home Conf", "@home_conf"),
                                       ("Week", "@week")])
    p.add_tools(g1_hover)
    
    g2 = Square(x='home_favBy', y='home_ptd', 
                size='marker_size', fill_color="navy",
                line_width=0.5,
                fill_alpha=0.5)
    g2_r = p.add_glyph(source_or_glyph=source_nfc, glyph=g2)
    g2_hover = HoverTool(renderers=[g2_r],
                             tooltips=[("Game", "@away_short_name at @home_short_name"),
                                       ("Final Score", "@away_score - @home_score"),
                                       ("Home Line", "@home_line"),
                                       ("Home Conf", "@home_conf"),
                                       ("Week", "@week")])
    p.add_tools(g2_hover)
    
    
    p.multi_line([[-35, 0, 35], [0, 0, 0]], 
                 [[0, 0, 0], [-35, 0, 35]],
                 color="black", 
                 alpha=0.8, 
                 line_width=2
                )
    
    p.line([-30, 0, 30], [-30, 0, 30], line_width=2, line_dash=[4, 4])
    
    p.text(26, 1, text=["Win SUP"], text_font_size="8pt", text_color="darkblue")
    p.text(26, -3, text=["Lose SUP"], text_font_size="8pt", text_color="dodgerblue")
    
    p.text(23, 24, text=["Win ATS"], text_font_size="8pt", text_color="black", angle=pi/4)
    p.text(25, 22, text=["Lose ATS"], text_font_size="8pt", text_color="red", angle=pi/4)
    
    
    p.xaxis.axis_label = "Home Team Favored By"
    p.xaxis.axis_label_text_font_size = "12pt"
    
    p.yaxis.axis_label = "Home Team Points Difference"
    p.yaxis.axis_label_text_font_size = "12pt"
    
    # p.legend.location = "top_left"
    
    # legend = Legend(legends=[
    #     ("sin(x)",   [g1_r]),
    #     ("2*sin(x)", [g2_r])
    # ], location=(0, -30))
    
    # p.add_layout(legend, 'right')
    
    # show the results
    show(p)

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

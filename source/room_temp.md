---
title: room_temp
date: 2020-05-07
---
Example Python program room_temp.py

## Modules

* In [1]: import pandas as pd
* In [12]: import matplotlib.pyplot as plt
* In [24]: import bearcart

## Code

Python example

    In [1]: import pandas as pd
    In [2]: df1=pd.read_csv("1.csv", index_col=1, parse_dates=True)
    In [3]: df2=pd.read_csv("2.csv", index_col=1, parse_dates=True)
    In [4]: df1.head(5)
    Out[4]: 
                         id   temp  pir  reed
    timestamp                                
    2012-01-16 16:46:28   0  23.25    1     0
    2012-01-16 16:46:29   1  23.10    1     0
    2012-01-16 16:46:30   2  23.20    0     0
    2012-01-16 16:46:30   3  23.25    0     0
    2012-01-16 16:46:31   4  23.25    1     0
    
    [5 rows x 4 columns]
    
    In [5]: df2.head(5)
    Out[5]: 
                         id   temp  pir  reed
    timestamp                                
    2012-01-16 16:46:27   0  19.90    0     1
    2012-01-16 16:46:28   1  19.95    0     1
    2012-01-16 16:46:29   2  20.00    0     1
    2012-01-16 16:46:30   3  19.70    0     1
    2012-01-16 16:46:31   4  20.00    0     1
    
    [5 rows x 4 columns]
    
    In [6]: df1_temp_downsampled=df1["temp"].resample(rule="1min",how="mean")
    In [7]: df2_temp_downsampled=df2["temp"].resample(rule="1min",how="mean")
    In [8]: df1_temp_downsampled.head(5)
    Out[8]: 
    timestamp
    2012-01-16 16:46:00    23.185366
    2012-01-16 16:47:00    23.122436
    2012-01-16 16:48:00    23.068590
    2012-01-16 16:49:00    23.053896
    2012-01-16 16:50:00    23.061538
    Freq: T, Name: temp, dtype: float64
    
    In [9]: %matplotlib qt
    In [10]: df1_temp_downsampled.plot()
    Out[10]: <matplotlib.axes.AxesSubplot at 0x1c763e10>
    
    In [11]: df2_temp_downsampled.plot()
    Out[11]: <matplotlib.axes.AxesSubplot at 0x1c763e10>
    
    In [12]: import matplotlib.pyplot as plt
    
    In [16]: df2_temp_downsampled.plot(label="Room 2")
    Out[16]: <matplotlib.axes.AxesSubplot at 0x1cf3c110>
    
    In [17]: df1_temp_downsampled.plot(label="Room 1")
    Out[17]: <matplotlib.axes.AxesSubplot at 0x1fe0e690>
    
    In [18]: df2_temp_downsampled.plot(label="Room 2")
    Out[18]: <matplotlib.axes.AxesSubplot at 0x1fe0e690>
    
    In [19]: plt.legend()
    Out[19]: <matplotlib.legend.Legend at 0x1cf1bbd0>
    
    In [20]: plt.ylabel("Temp (Celsius)")
    Out[20]: <matplotlib.text.Text at 0x1fe90590>
    
    In [21]: plt.savefig("temp_comparison.png")
    
    In [24]: import bearcart
    
    In [25]: df_temp = pd.DataFrame({'Room 1':df1_temp_downsampled, 'Room 2':df2_temp_downsampled})
    
    In [26]: df_temp.head(5)
    Out[26]: 
                            Room 1     Room 2
    timestamp                                
    2012-01-16 16:46:00  23.185366  19.966667
    2012-01-16 16:47:00  23.122436  19.957692
    2012-01-16 16:48:00  23.068590  19.956494
    2012-01-16 16:49:00  23.053896  19.968590
    2012-01-16 16:50:00  23.061538  19.972388
    
    [5 rows x 2 columns]
    
    In [28]: html_path = r'index.html'
    
    In [29]: data_path = r'data.json'
    
    In [30]: js_path = r'rickshaw.min.js'
    
    In [31]: css_path = r'rickshaw.min.css'
    
    In [36]: vis = bearcart.Chart(df_temp[df_temp.index.month==4].resample(rule="15min"))
    
    In [37]: vis.create_chart(html_path=html_path, data_path=data_path,
                     js_path=js_path, css_path=css_path)
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

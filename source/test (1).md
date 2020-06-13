---
title: test (1)
date: 2020-05-07
---
Example Python program test (1).py

## Modules

* import matplotlib.pyplot as plt
* import matplotlib.image as mpimg
* import numpy as np
* import glob
* import os
* import mysql.connector
* import matplotlib
* import matplotlib.pyplot as plt
* import numpy
* from numpy import *
* from numpy.polynomial import Polynomial
* from scipy.signal import argrelextrema

## Code

Python example

    import matplotlib.pyplot as plt
    import matplotlib.image as mpimg
    import numpy as np
    import glob
    import os
    import mysql.connector
    import matplotlib
    import matplotlib.pyplot as plt
    
    import numpy
    from numpy import *
    from numpy.polynomial import Polynomial
    from scipy.signal import argrelextrema
    
    cnx = mysql.connector.connect(user='xxx', password='xxx', database='ASTOR')
    cursor = cnx.cursor()
    
    
    """
    mysql> desc eucrib;
    +--------+---------+------+-----+---------+-------+
    | Field  | Type    | Null | Key | Default | Extra |
    +--------+---------+------+-----+---------+-------+
    | id     | int(11) | NO   | PRI | NULL    |       |
    | min    | float   | YES  |     | NULL    |       |
    | max    | float   | YES  |     | NULL    |       |
    | mean   | float   | YES  |     | NULL    |       |
    | median | float   | YES  |     | NULL    |       |
    | std    | float   | YES  |     | NULL    |       |
    +--------+---------+------+-----+---------+-------+
    """
    
    query = ("SELECT id, mean FROM gama")
    cursor.execute(query)
    
    x = []
    y = []
    for item in cursor:
        x.append(item[0])
        y.append(item[1])
    #print cursor.fetchall()
    
    ys = np.array(y)
    xs = np.array(x)
    
    p = Polynomial.fit(x, y, 6)
    
    
    plt.plot(*p.linspace())
    plt.show()
    
    plt.close()
    
    cursor.close()
    cnx.close()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

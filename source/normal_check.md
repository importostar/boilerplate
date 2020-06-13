---
title: normal_check
date: 2020-05-07
---
Example Python program normal_check.py

## Modules

* import numpy as np
* import matplotlib
* import matplotlib.pyplot as plt
* from pandas_datareader import data as pdr
* from datetime import date, timedelta
* import matplotlib.mlab as mlab

## Methods

* def get_index(index):
* def normal_check(dataframe):

## Code

Python example

    # -*- coding: utf-8 -*-
    """
    Retornos y Distribución Normal
    Autor: Guillermo Izquierdo
    Este código es para fines educativos exclusivamente
    
    """
    
    
    import numpy as np
    import matplotlib
    import matplotlib.pyplot as plt
    from pandas_datareader import data as pdr
    from datetime import date, timedelta
    import matplotlib.mlab as mlab
    matplotlib.style.use('ggplot')
    
    
    def get_index(index):
        # Definimos las fechas de nuestro indice
        today = date.today()
        day = timedelta(days=1)
        today2 = today - day
        enddate = today2.isoformat()
        years = timedelta(weeks=52)
        period = today - years
        startdate = period.isoformat()
        # Definimos el indice que queremos descargar
        index = index
        # Obtenemos los datos usando pandas_datareader
        #Dividimos los datos en dos, precios y retornos
        data = pdr.get_data_yahoo(index, start=startdate, end=enddate)
        data['returns'] = data['Close'].pct_change()
        data = data.dropna()
        prices = data['Close']
        returns = data['returns']
        return [prices, returns]
    
    
    def normal_check(dataframe):
        count, bins, ignored = plt.hist(
            dataframe, 100, normed=True, align='mid', color='blue', label='Histograma')
        # Calculamos las medidas de tendencia central
        mu = np.mean(dataframe)
        sigma = np.std(dataframe)
        # Generamos la linea de distribución normal
        x = mlab.normpdf(bins, mu, sigma)
        plt.plot(bins, x, color='r', lw=4)
        plt.title("Distribución Normal de los Retornos")
        plt.xlabel("Retornos")
        plt.ylabel("Frecuencia")
        plt.legend()
        plt.show()
        
    index = '^MXX'
    indice = get_index(index)
    normal_check(indice[1])

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

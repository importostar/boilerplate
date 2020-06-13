---
title: qtcharts percentbarchart example
date: 2020-05-07
---
Example Python program qtcharts-percentbarchart-example.py
This program creates a PyQt GUI

## Modules

* from PyQt5.QtChart import *
* from PyQt5.QtGui import *
* from PyQt5.QtCore import *
* from PyQt5.QtWidgets import *

## Code

Example Python PyQt program :

    # from: https://doc.qt.io/qt-5/qtcharts-percentbarchart-example.html
    from PyQt5.QtChart import *
    from PyQt5.QtGui import *
    from PyQt5.QtCore import *
    from PyQt5.QtWidgets import *
    
    a = QApplication([])
    
    set0 = QBarSet("Jane")
    set1 = QBarSet("John")
    set2 = QBarSet("Axel")
    set3 = QBarSet("Mary")
    set4 = QBarSet("Samantha")
    
    set0 << 1 << 2 << 3 << 4 << 5 << 6
    set1 << 5 << 0 << 0 << 4 << 0 << 7
    set2 << 3 << 5 << 8 << 13 << 8 << 5
    set3 << 5 << 6 << 7 << 3 << 4 << 5
    set4 << 9 << 7 << 5 << 3 << 1 << 2
    
    series = QPercentBarSeries()
    series.append(set0)
    series.append(set1)
    series.append(set2)
    series.append(set3)
    series.append(set4)
    
    chart = QChart()
    chart.addSeries(series)
    chart.setTitle("Simple percentbarchart example")
    chart.setAnimationOptions(QChart.SeriesAnimations)
    
    categories = ["Jan", "Feb", "Mar", "Apr", "May", "Jun"]
    axis = QBarCategoryAxis()
    axis.append(categories)
    chart.createDefaultAxes()
    chart.setAxisX(axis, series)
    
    chart.legend().setVisible(True)
    chart.legend().setAlignment(Qt.AlignBottom)
    
    chartView = QChartView(chart)
    chartView.setRenderHint(QPainter.Antialiasing)
    
    window = QMainWindow()
    window.setCentralWidget(chartView)
    window.resize(420, 300)
    window.show()
    
    a.exec_()
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/

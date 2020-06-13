---
title: test_qtcharts
date: 2020-05-07
---
Example Python program test_qtcharts.py
This program creates a PyQt GUI
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* from qgis.core import QgsVectorLayer, QgsFeatureRequest, QgsExpression
* from PyQt5.QtCore import QPointF, QVariant, Qt
* from PyQt5.QtWidgets import QWidget, QVBoxLayout, QHBoxLayout, QPushButton
* from PyQt5.QtChart import QLineSeries, QChart, QChartView, QDateTimeAxis, QValueAxis
* import numpy as np
* import sys
* from qgis.core import QgsApplication
* from PyQt5.QtWidgets import QApplication

## Classes

* class MyPlot(QWidget):

## Methods

* def series_to_polyline(xdata, ydata):
* def __init__(self, parent=None):
* def add_data(self, data):
* def on_zoom_in(self):
* def on_zoom_out(self):

## Code

Example Python PyQt program :

    from qgis.core import QgsVectorLayer, QgsFeatureRequest, QgsExpression
    
    from PyQt5.QtCore import QPointF, QVariant, Qt
    from PyQt5.QtWidgets import QWidget, QVBoxLayout, QHBoxLayout, QPushButton
    
    from PyQt5.QtChart import QLineSeries, QChart, QChartView, QDateTimeAxis, QValueAxis
    
    import numpy as np
    
    def series_to_polyline(xdata, ydata):
        """Convert series data to QPolygon(F) polyline
        
        This code is derived from PythonQwt's function named 
        `qwt.plot_curve.series_to_polyline`"""
        size = len(xdata)
        polyline = QPolygonF(size)
        pointer = polyline.data()
        dtype, tinfo = np.float, np.finfo  # integers: = np.int, np.iinfo
        pointer.setsize(2*polyline.size()*tinfo(dtype).dtype.itemsize)
        memory = np.frombuffer(pointer, dtype)
        memory[:(size-1)*2+1:2] = xdata
        memory[1:(size-1)*2+2:2] = ydata
        return polyline
    
    class MyPlot(QWidget):
        def __init__(self, parent=None):
            QWidget.__init__(self, parent)
            vbox = QVBoxLayout()
            hbox = QHBoxLayout()
            self.__zoom_in_btn = QPushButton("Zoom In")
            self.__zoom_out_btn = QPushButton("Zoom Out")
    
            self.__zoom_in_btn.clicked.connect(self.on_zoom_in)
            self.__zoom_out_btn.clicked.connect(self.on_zoom_out)
    
            self.__chart = QChart()
            self.__chart.legend().hide()
            chart_view = QChartView(self.__chart, self)
    
            hbox.addWidget(self.__zoom_in_btn)
            hbox.addWidget(self.__zoom_out_btn)
            vbox.addLayout(hbox)
            vbox.addWidget(chart_view)
    
            self.setLayout(vbox)
            self.resize(800,400)
    
        def add_data(self, data):
            series = QLineSeries(self)
            print("append data")
            for dt, val in data:
                if isinstance(dt, QVariant) and dt.isNull():
                    continue
                series.append(QPointF(dt.toMSecsSinceEpoch(), val))
    
            self.__chart.addSeries(series)
            self.__chart.setTitle("Water conductivity over time")
    
            date_axis = QDateTimeAxis()
            date_axis.setFormat("dd/MM/yyyy HH:mm")
            self.__chart.addAxis(date_axis, Qt.AlignBottom)
            series.attachAxis(date_axis)
    
            value_axis = QValueAxis()
            value_axis.setMin(0.0)
            value_axis.setMax(1.0)
            self.__chart.addAxis(value_axis, Qt.AlignLeft)
            series.attachAxis(value_axis)
    
            #series.setPointLabelsFormat("@yPoint")
            #series.setPointLabelsVisible(True)
            series.setUseOpenGL(True)        
    
        def on_zoom_in(self):
            self.__chart.zoomIn()
        def on_zoom_out(self):
            self.__chart.zoomOut()
            
    
    if __name__=='__main__':
        import sys
    
        from qgis.core import QgsApplication
        from PyQt5.QtWidgets import QApplication
    
        app = QgsApplication([s.encode('utf8') for s in sys.argv], True)
        #app = QApplication(sys.argv)
        QgsApplication.initQgis()
    
        measure_layer = QgsVectorLayer('service=bdlhes key="station_id,measure_time" table="measure"."water_conductivity"', "measure_layer", "postgres")
        req = QgsFeatureRequest(QgsExpression("station_id={}".format(2)))
        print("data from db")
        data = [(f["measure_time"], f["measure"]) for f in measure_layer.getFeatures(req)]
    
        p = MyPlot()
        p.add_data(data)
    
        print("render")
        p.show()
            
        app.exec_()
    
        QgsApplication.exitQgis()
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/

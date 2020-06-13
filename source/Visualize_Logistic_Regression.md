---
title: Visualize_Logistic_Regression
date: 2020-05-07
---
Example Python program Visualize_Logistic_Regression.py
This program creates a PyQt GUI
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import sys
* from PyQt5.QtWidgets import QApplication, QWidget, QGridLayout, QPushButton, QHBoxLayout
* from PyQt5 import QtGui
* import pyqtgraph as pg
* import numpy as np
* from PyQt5 import QtCore
* import time

## Classes

* class MainWindow(QWidget):
* class Plotter(QtCore.QThread):

## Methods

* 	def __init__(self):
* 	def btn_clicked_slot(self, thread):
* 	def drawPoints(self, x_0, x_1):
* 	def moseMoved(self, evt):
* 	def clicked(plot, points):
* 	def __init__(self, min_0, max_0, min_1, max_1):
* 	def run(self):

## Code

Example Python PyQt program :

    
    import sys
    from PyQt5.QtWidgets import QApplication, QWidget, QGridLayout, QPushButton, QHBoxLayout
    from PyQt5 import QtGui
    import pyqtgraph as pg
    import numpy as np
    from PyQt5 import QtCore
    import time
    
    class MainWindow(QWidget):
    	def __init__(self):
    		super().__init__()
    
    		##### ranges of inputs
    
    		self.min_0 = 0
    		self.min_1 = 1
    		self.max_0 = .8
    		self.max_1 = 1.8
    
    		#############	
    
    		layout = QGridLayout()
    		self.setLayout(layout)
    
    		self.plotterThread = Plotter(self.min_0, self.max_0, self.min_1, self.max_1)
    		self.plotterThread.plotSignal.connect(self.drawPoints)
    
    		#### .. toolbar
    		panel_toolbar = QWidget()
    		layout_toolbar = QHBoxLayout()
    		panel_toolbar.setLayout(layout_toolbar)
    
    		btn = QPushButton("Click")
    		layout_toolbar.addWidget(btn)
    		layout_toolbar.addStretch()
    
    		layout.addWidget(panel_toolbar)
    
    		btn.clicked.connect(lambda: self.btn_clicked_slot(self.plotterThread))
    
    		#### graph
    		pg.setConfigOption('background', 'w')
    
    
    		graph = pg.GraphicsLayoutWidget()
    		layout.addWidget(graph)
    
    		self.plot = graph.addPlot()
    		#splot.plot([0, 1, 2, 3, 4],[0, 1, 2, 3, 10], pen=(0,0,200), symbolBrush=(0,0,200), symbolPen='w', symbol='o', symbolSize=14, name="symbol='o'")
    
    		xAxisMin = self.min_0
    		xAxisMax = self.max_1
    
    		yAxisMin = 0
    		yAxisMax = 1
    		self.plot.setXRange(xAxisMin, xAxisMax, padding = .1)
    		self.plot.setYRange(yAxisMin, yAxisMax, padding = .1)
    
    		self.pp = pg.SignalProxy(self.plot.scene().sigMouseMoved, rateLimit= 60, slot = self.moseMoved)
    
    		self.scatter_0 = pg.ScatterPlotItem(pen=None, brush=(255, 0, 0), symbol ='o', size = 17)
    		self.scatter_0.setZValue(2)
    		self.scatter_1 = pg.ScatterPlotItem(pen=None, brush=(0,255,0), symbol ='t', size = 17)
    		self.plot.addItem(self.scatter_0)
    		self.plot.addItem(self.scatter_1)
    
    
    		self.scatter_range = pg.ScatterPlotItem()
    
    		self.scatter_range_1_min = pg.ScatterPlotItem(pen=None, brush=pg.mkBrush(0, 255, 0, 45), symbol ='t3', size = 30)
    		self.scatter_range_1_max = pg.ScatterPlotItem(pen=None, brush=pg.mkBrush(0, 255, 0, 45), symbol ='t2', size = 30)
    
    		self.scatter_range.addPoints([{"pos": (self.min_0,0), "symbol" :'t3'}])
    		self.scatter_range.points()[0].tag = 0
    		self.scatter_range.addPoints([{"pos": (self.max_0,0), "symbol" :'t2'}])
    		self.scatter_range.points()[1].tag = 1
    		self.scatter_range.addPoints([{"pos": (self.min_1,1), "symbol" :'t3'}])
    		self.scatter_range.points()[2].tag = 2
    		self.scatter_range.addPoints([{"pos": (self.max_1,1), "symbol" :'t2'}])
    		self.scatter_range.points()[3].tag = 3
    		self.plot.addItem(self.scatter_range)
    
    
    		self.brush_default = [pg.mkBrush(255, 0, 0, 45), pg.mkBrush(255, 0, 0, 45), pg.mkBrush(0,255,  0, 45), pg.mkBrush(0,255,  0, 45)]
    		self.scatter_range.setBrush(self.brush_default)
    		self.scatter_range.setPen(None)
    		self.scatter_range.setSize(30)
    
    		self.pen_default_x_0 = []
    		self.pen_default_x_1 = []
    
    
    	def btn_clicked_slot(self, thread):
    		thread.start()
    
    	def drawPoints(self, x_0, x_1):
    		self.scatter_0.addPoints(x = [x_0], y = [0])
    		self.scatter_0.points()[len(self.scatter_0.points()) - 1].tag = len(self.scatter_0.points())
    		self.pen_default_x_0.append(None)
    
    		self.scatter_1.addPoints(x = [x_1], y = [1])
    		self.scatter_1.points()[len(self.scatter_1.points()) - 1].tag = len(self.scatter_1.points())
    		self.pen_default_x_1.append(None)
    
    
    	def moseMoved(self, evt):
    
    		pos = evt[0]
    		if self.plot.sceneBoundingRect().contains(pos):
    			
    			mousePoint = self.plot.vb.mapSceneToView(pos)
    
    
    			self.scatter_0.setPen(self.pen_default_x_0)
    			points = self.scatter_0.pointsAt(mousePoint)
    			
    			for point in points:
    				pen_temp = self.pen_default_x_0[:]
    				pen_temp[point.tag - 1] = pg.mkPen(color=(0, 0, 0), width = 3)
    
    				self.scatter_0.setPen(pen_temp)
    				return
    
    			self.scatter_1.setPen(self.pen_default_x_1)
    			points = self.scatter_1.pointsAt(mousePoint)
    			for point in points:
    				pen_temp = self.pen_default_x_1[:]
    				pen_temp[point.tag - 1] = pg.mkPen(color=(0, 0, 0), width = 3)
    
    				self.scatter_1.setPen(pen_temp)
    				return
    
    
    			points = self.scatter_range.pointsAt(mousePoint)
    			self.scatter_range.setBrush(self.brush_default)
    				
    			for point in points:
    				bursh_temp = self.brush_default[:]
    				if point.tag <= 1:
    					bursh_temp[point.tag] = pg.mkBrush(255, 0, 0, 255)
    				elif point.tag <= 3:
    					bursh_temp[point.tag] = pg.mkBrush(0, 255, 0, 255)
    
    				self.scatter_range.setBrush(bursh_temp)
    				
    	def clicked(plot, points):
    	    print("clicked points", points)
    
    
    class Plotter(QtCore.QThread):
    
    	plotSignal = QtCore.pyqtSignal(float, float)
    
    	def __init__(self, min_0, max_0, min_1, max_1):
    		super().__init__()
    
    		self.min_0 = min_0
    		self.max_0 = max_0
    
    		self.min_1 = min_1
    		self.max_1 = max_1
    
    
    	def run(self):
    
    		print("starting...")
    
    		x_0_range = self.max_0 - self.min_0
    		x_1_range = self.max_1 - self.min_1
    		
    		no_of_points = 10
    		x_0 = (np.random.rand(no_of_points) * x_0_range) + self.min_0
    		x_1 = (np.random.rand(no_of_points) * x_1_range) + self.min_1
    
    		for i in range(no_of_points):
    			self.plotSignal.emit(x_0[i], x_1[i])
    			time.sleep(0.1)
    			print("here", x_0[i], x_1[i])
    
    
    if __name__ == '__main__':
    	app = QApplication(sys.argv)
    
    	win = MainWindow()
    	win.show()
    
    	app.exec_()

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/

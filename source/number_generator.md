---
title: number_generator
date: 2020-05-07
---
Example Python program number_generator.py
This program creates a PyQt GUI
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import numpy as np
* import pyqtgraph as pg
* import sys
* from PyQt5.QtWidgets import QWidget, QApplication, QGridLayout, QHBoxLayout, QPushButton, QTabWidget,QPlainTextEdit
* from PyQt5 import QtCore

## Classes

* class DataPoint(pg.PlotDataItem):
* class MainWindow(QWidget):

## Methods

* 	def __init__(self, parent, shape, color):
* 	def pointClicked(self):
* 	def __init__(self):
* 	def mouseClicked(self, evt):
* 	def update_data_table(self):
* 	def mouseMoved(self, evt):

## Code

Example Python PyQt program :

    import numpy as np
    import pyqtgraph as pg
    import sys
    from PyQt5.QtWidgets import QWidget, QApplication, QGridLayout, QHBoxLayout, QPushButton, QTabWidget,QPlainTextEdit
    from PyQt5 import QtCore
    
    
    class DataPoint(pg.PlotDataItem):
    
    	def __init__(self, parent, shape, color):
    		super().__init__()
    
    		super().setData(symbol = shape, pen = color, symbolBrush = color, symbolPen = 'w', symbolSize = 16)
    
    		self.parent = parent
    
    		#self.sigClicked.connect(self.pointClicked)
    		print("ksaf")
    
    	def pointClicked(self):
    
    		print("sigClicked")
    
    		if not self.parent.isDeleting:
    			return
    
    class MainWindow(QWidget):
    
    	isDeleting = False
    
    	all_points = {}
    
    	xAxisMin = -5; xAxisMax = 5
    	yAxisMin = -5; yAxisMax = 5
    
    	def __init__(self):
    		super().__init__()
    
    		layoutMain = QGridLayout()
    		layoutMain.setContentsMargins(0, 0, 0, 0)
    		self.setLayout(layoutMain)
    
    		panelToolbar = QWidget()
    		layoutToolbar = QHBoxLayout()
    		panelToolbar.setLayout(layoutToolbar)
    
    
    		btnClick = QPushButton("Click")
    		layoutToolbar.addWidget(btnClick, alignment =QtCore.Qt.AlignLeft)
    
    		panelGraph = pg.GraphicsLayoutWidget()
    		pg.setConfigOptions(antialias=True)
    
    		self.plot = panelGraph.addPlot()
    		self.plot.disableAutoRange()
    		self.plot.hideButtons()
    
    		xAxis = pg.InfiniteLine(pen=pg.mkPen((200, 0, 0,), width = 2))
    		xAxis.setAngle(0)
    		xAxis.setValue((0, 0))
    		xAxis.setZValue(1)
    		self.plot.addItem(xAxis)
    
    		yAxis = pg.InfiniteLine(pen=pg.mkPen((0, 200, 0), width=2))
    		yAxis.setAngle(90)
    		yAxis.setValue((0, 0))
    		yAxis.setZValue(1)
    		self.plot.addItem(yAxis)
    		
    		self.plot.setXRange(self.xAxisMin, self.xAxisMax, padding = 0)
    		self.plot.setYRange(self.yAxisMin, self.yAxisMax, padding = 0)
    		self.plot.setAspectLocked()
    		self.plot.showGrid(True, True)
    		self.plot.getAxis("left").setTickSpacing(5, 1)
    		self.plot.getAxis("bottom").setTickSpacing(5, 1)
    
    		self.movingPoint = DataPoint(self, 'o', (0, 200, 0))
    
    		self.pp = pg.SignalProxy(self.plot.scene().sigMouseMoved, rateLimit=60, slot=self.mouseMoved)
    		self.pp1 = pg.SignalProxy(self.plot.scene().sigMouseClicked, rateLimit=60, slot=self.mouseClicked)
    		
    
    		self.tabs = QTabWidget()
    		self.tab1 = QPlainTextEdit()
    
    		self.tabs.addTab(self.tab1, "o")
    
    		layoutMain.addWidget(panelToolbar, 0, 0, 1, 2)
    		layoutMain.addWidget(panelGraph, 1, 0)
    		layoutMain.addWidget(self.tabs, 1, 1)
    
    
    	def mouseClicked(self, evt):
    
    		if self.isDeleting:
    			return
    
    		pos = evt[0]
    
    		try:
    			
    			shape = "o"
    
    			point = DataPoint(self, shape, (0, 200, 0))
    			point.setZValue(2)
    			point.setData([pos.pos().x()],[pos.pos().y()])
    			
    
    			if shape in self.all_points:
    				self.all_points[shape].append(point)
    			else:
    				self.all_points[shape] = [point]
    			self.plot.addItem(point)
    			
    		except:
    			print("error")
    
    		self.update_data_table()
    
    	def update_data_table(self):
    
    		self.tab1.clear()
    		
    		for key in self.all_points.keys():
    			text = ""
    			text1 = ""
    			for item in self.all_points[key]:
    				
    				text += str(int(item.getData()[0][0])) + ", "
    				text1 += str(int(item.getData()[1][0])) + ", "
    
    			text = text[:-2]
    			text1 = text1[:-2]
    			self.tab1.appendPlainText(text)
    			self.tab1.appendPlainText(text1)
    
    
    	def mouseMoved(self, evt):
    	
    		pos = evt[0]
    			
    		if self.plot.sceneBoundingRect().contains(pos):
    			
    			mousePoint = self.plot.vb.mapSceneToView(pos)
    			self.movingPoint.setData([mousePoint.x()],[mousePoint.y()])
    			self.plot.addItem(self.movingPoint)
    if __name__ == '__main__':
    	app = QApplication(sys.argv)
    	win = MainWindow()
    
    	win.show()
    
    	app.exec_()

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/

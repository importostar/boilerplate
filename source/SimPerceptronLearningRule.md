---
title: SimPerceptronLearningRule
date: 2020-05-07
---
Example Python program SimPerceptronLearningRule.py
This program creates a PyQt GUI
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import sys
* import pyqtgraph as pg
* import numpy as np
* from PyQt5.QtWidgets import QApplication, QWidget, QPushButton, QHBoxLayout,QComboBox, QGroupBox, QDialog, QVBoxLayout, QGridLayout
* from PyQt5 import QtCore
* from PyQt5 import QtGui
* from PyQt5.QtCore import QObject, pyqtSlot, pyqtSignal
* import copy
* import time
* import numpy as np

## Classes

* class DataPoint(pg.PlotDataItem):
* class LegendRow():
* class AlgorithmRunner(QtCore.QThread):
* class MainWindow(QWidget):

## Methods

* 	def __init__(self, parent, shape, color, *args, **kwargs):
* 	def pointClicked(obj):
* 	def getShape(self):
* 	def getColor(self): # return tuple eg. (255,255,255)
* 	def setSymbolPen(self, pen):
* 	def reassignData(self, pen):
* 	def __init__(self, x, y, symbol, color):
* 	def __init__(self, parent):
* 	def run(self):
* 	def hardLimit(self, x):
* 	def __init__(self):
* 	def updateUiForResult(self, weight_vector, theta, y_at_x_0, vector, isResult):
* 	def highlightPoint(self, point, lastPoint):
* 	def clickedRunAlgo(self):
* 	def btnDelClicked(self):
* 	def btnClearAllClicked(self):
* 	def comboIndexChanged(self):
* 	def clickTestEvnet(self):
* 	def mouseClicked(self, evt):
* 	def updateLegend(self):
* 	def mouseMoved(self, evt):

## Code

Example Python PyQt program :

    import sys
    import pyqtgraph as pg
    import numpy as np
    from PyQt5.QtWidgets import QApplication, QWidget, QPushButton, QHBoxLayout,QComboBox, QGroupBox, QDialog, QVBoxLayout, QGridLayout
    from PyQt5 import QtCore
    from PyQt5 import QtGui
    from PyQt5.QtCore import QObject, pyqtSlot, pyqtSignal
    import copy
    import time
    import numpy as np
    
    xAxisMin = -5; xAxisMax = 5
    yAxisMin = -5; yAxisMax = 5
    
    class DataPoint(pg.PlotDataItem):
    	
    	def __init__(self, parent, shape, color, *args, **kwargs):
    		super().__init__(*args, **kwargs)
    		super().setData(pen=color, symbolBrush=color, symbolPen='w', symbolSize=16, name="symbol='t'")
    		super().setData(symbol=shape)
    		
    		self.shape = shape
    		self.color = color
    		self.parentObject = parent
    
    		self.sigClicked.connect(lambda: DataPoint.pointClicked(self))
    	
    	@staticmethod
    	def pointClicked(obj):
    		
    		if(not MainWindow.isDeleting):
    			return
    		
    		obj.parentObject.plot.removeItem(obj)
    		
    		for list in obj.parentObject.allPoints:
    			if(list[0].getShape() == obj.getShape()):
    				list.remove(obj)
    			
    				if(len(list) == 0):
    					obj.parentObject.allPoints.remove(list)
    		obj.parentObject.updateLegend()
    		
    	def getShape(self):
    		return self.shape
    			
    	def getColor(self): # return tuple eg. (255,255,255)
    		return self.color
    		
    	def setSymbolPen(self, pen):
    		self.setData(symbolPen = pen)
    	
    	
    	def reassignData(self, pen):
    		super().setData(symbol=self.shape, symbolPen =pen, symbolBrush = self.color, pen = self.color, symbolSize=16)
    
    class LegendRow():
    	def __init__(self, x, y, symbol, color):
    		self.labelPoint = pg.PlotDataItem(x,y ,symbol = symbol, symbolBrush = color)
    		self.labelText = pg.TextItem("1")
    		self.labelText.setPos(x[0] + 10, y[0] - 12)
    
    	
    class AlgorithmRunner(QtCore.QThread):
    	
    	update_signal = QtCore.pyqtSignal(object, float, float, object, bool)
    	highlight_signal = QtCore.pyqtSignal(object, object)
    	lastPoint = None
    	final_vector = None
    	
    	def __init__(self, parent):
    		QtCore.QThread.__init__(self)
    		self.parent = parent
    		
    	def run(self):
    		iteration = 0
    		no_all_points = 0
    		ok_count = 0
    		old_weight = (0,0,0)
    		theta = 0
    		y_at_x_0 = 0
    		for list in self.parent.allPoints:
    			no_all_points = no_all_points +  len(list)
    		
    		while ok_count < no_all_points:
    			class_to_test = iteration % 2
    			for i in range(len(self.parent.allPoints[class_to_test])):
    			
    				v_to_test = (self.parent.allPoints[class_to_test][i].xData[0], self.parent.allPoints[class_to_test][i].yData[0], 1)
    				
    				e = class_to_test - self.hardLimit(np.dot(old_weight, v_to_test))
    				
    				if e == 0:
    					ok_count = ok_count + 1
    					if i == len(self.parent.allPoints[class_to_test]) - 1:
    						iteration = iteration + 1
    					continue
    				
    				old_weight = np.add(old_weight, np.multiply(e, v_to_test))
    				
    				iteration = iteration + 1
    				ok_count = 0
    				
    				a = old_weight[0];b = old_weight[1];B = old_weight[2]
    				y_at_x_0 = -B / b
    				theta = ( np.arctan((b / a)) * 180 / np.pi) 
    				
    				theta = theta + 270
    				
    				## calcualate vector...
    				
    				vector = old_weight[0:2]
    				norm = np.sqrt(np.dot(vector, vector))
    				unit_vector = np.divide(vector, norm)
    				self.final_vector = np.multiply(unit_vector, -B / norm)
    				
    				####
    				self.highlight_signal.emit(self.parent.allPoints[class_to_test][i] ,self.lastPoint)
    				self.lastPoint = self.parent.allPoints[class_to_test][i]
    				self.update_signal.emit(old_weight, theta, y_at_x_0, self.final_vector, False)
    				
    				self.sleep(1)
    				
    				break
    	
    		self.update_signal.emit(old_weight, theta, y_at_x_0,self.final_vector, True)
    
    		self.highlight_signal.emit(None, self.lastPoint)
    
    		self.lastPoint = None
    		
    	def hardLimit(self, x):
    		if x < 0:
    			return 0
    		else:
    			return 1
    	
    class MainWindow(QWidget):
    		
    	maxNumberOfClass = 2
    	
    	hLines = []
    	vLines = []
    	
    	currentIndex = 0
    	allPoints = []
    	
    	combo_icons = ["o", "d", "star", "+", "h", "p", "s", "t1"]
    	point_colors = {"o":(0,0,200), "t1":(0,128,0), "s":(54,55,55), "p":(0,114,189), "h":(217,83,25), "star":(237,177,32), "+":(126,47,142), "d":(119,172,48)}
    	
    	label_icons = []
    	label_counts = []
    	
    	isDeleting = False
    	
    	decision_boundary = pg.InfiniteLine(pen=pg.mkPen((0,80, 110), width=2.5))
    	
    	def __init__(self):
    		super().__init__()
    		
    		layoutMain = QGridLayout()
    		layoutMain.setContentsMargins(5, 10, 5, 5)
    		self.setLayout(layoutMain)
    
    		# Toolbar 
    		panelToolbar = QWidget()
    		layoutToolbar = QHBoxLayout()
    		layoutToolbar.setContentsMargins(0, 0, 0, 0)
    		panelToolbar.setLayout(layoutToolbar)
    
    		btnHome = QPushButton("Home")
    		btnHome.clicked.connect(self.clickTestEvnet)
    		
    		btnRunAlgo = QPushButton("Run Algorithm")
    		btnRunAlgo.clicked.connect(self.clickedRunAlgo)
    		
    		self.btnDel = QPushButton("Delete")
    		self.btnDel.clicked.connect(self.btnDelClicked)
    		
    		self.btnClearAll = QPushButton("Clear All")
    		self.btnClearAll.clicked.connect(self.btnClearAllClicked)
    		
    		self.shape_combo = QComboBox()
    		self.shape_combo.addItem("circle")
    		self.shape_combo.addItem("diamond")
    		self.shape_combo.addItem("star")
    		self.shape_combo.addItem("plus")
    		self.shape_combo.addItem("six")
    		self.shape_combo.addItem("five")
    		self.shape_combo.addItem( "square")
    		self.shape_combo.addItem("triangle")
    		
    		combo = QComboBox()
    		model = combo.model()
    		for row in range(10):
    			item = QtGui.QStandardItem("row")
    			font = item.font()
    			font.setPointSize(10)
    			item.setFont(font)
    			model.appendRow(item)
    
    		self.pointColorBtn = QPushButton()
    		self.pointColorBtn.setStyleSheet("background-color: red")
    
    
    		layoutToolbar.addWidget(btnHome) # Add panel to main gridlayout
    		layoutToolbar.addWidget(btnRunAlgo)
    		layoutToolbar.addStretch()
    		layoutToolbar.addWidget(self.shape_combo)
    		layoutToolbar.addWidget(self.pointColorBtn)
    		layoutToolbar.addWidget(self.btnDel, alignment  =QtCore.Qt.AlignLeft) # Add panel to main gridlayout
    		layoutToolbar.addWidget(self.btnClearAll)
    		
    		# Graphic Panel
    		mainGraphicPanel = pg.GraphicsLayoutWidget()
    		pg.setConfigOptions(antialias=True)
    		
    		self.plot = mainGraphicPanel.addPlot()
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
    
    		self.plot.setXRange(xAxisMin, xAxisMax, padding = 0)
    		self.plot.setYRange(yAxisMin, yAxisMax, padding = 0)
    		self.plot.setAspectLocked()
    		self.plot.showGrid(True, True)
    		self.plot.getAxis("left").setTickSpacing(5, 1)
    
    		self.plot.getAxis("bottom").setTickSpacing(5, 1)
    
    		self.pp = pg.SignalProxy(self.plot.scene().sigMouseMoved, rateLimit=60, slot=self.mouseMoved)
    		self.pp1 = pg.SignalProxy(self.plot.scene().sigMouseClicked, rateLimit=60, slot=self.mouseClicked)
    		
    		self.movingPoint = DataPoint(self,self.combo_icons[self.currentIndex], self.point_colors[self.combo_icons[self.currentIndex]])
    		self.movingPoint.setZValue(3)
    		self.shape_combo.currentIndexChanged.connect(self.comboIndexChanged)
    		
    		# add panels to mainPanel
    		layoutMain.addWidget(panelToolbar, 0, 0)
    		layoutMain.addWidget(mainGraphicPanel, 1, 0)
    		
    		# setting up threads
    		self.thread = AlgorithmRunner(self	)
    		self.thread.update_signal.connect(self.updateUiForResult)
    		self.thread.highlight_signal.connect(self.highlightPoint)
    		
    		# create remaining GUI
    		self.supporting_vector = pg.PlotDataItem(pen=pg.mkPen('r', width=3))
    		self.supporting_vector.setZValue(2)
    		self.arrowHead = pg.ArrowItem(angle = 0, brush = (255, 0,0), pen=pg.mkPen('r', width=2))
    		
    		self.result_label = pg.LabelItem()
    		
    		self.result_label.setText("<span style='font-size: 10pt; color :orange'>Weight<br/> </span>  <span style='font-size: 12pt;color: gray'>(%0.3f,%0.3f)</span> <br/><br/>  <span style='font-size: 10pt; color: orange'>Bias<br/></span><span style='font-size: 12pt;color:gray'>%0.3f</span>" % (0,0,0))
    		self.result_label.setPos(2,60)
    		
    		self.result_label.setParentItem(self.plot.getViewBox())
    		self.show()
    	
    	def updateUiForResult(self, weight_vector, theta, y_at_x_0, vector, isResult):
    		
    		if isResult:
    			self.decision_boundary.setPen(pg.mkPen((0, 255,0), width = 3))
    		self.decision_boundary.setAngle(theta)
    		
    		self.decision_boundary.setValue((0, y_at_x_0))
    		
    		if(vector[0] == 0 and vector[1] == 0):
    			self.supporting_vector.setData([0])
    		else:
    			self.supporting_vector.setData([0,vector[0]],[0,vector[1]])
    			
    		arrow_theta = theta- 270
    		if arrow_theta > 0:
    			if(vector[0] < 0):
    				arrow_theta = -(arrow_theta)
    			else:
    				arrow_theta = (360 - (arrow_theta)) + 180
    		else:
    			if(vector[0] < 0):
    				arrow_theta = abs(arrow_theta)
    			else:
    				arrow_theta = abs(arrow_theta) + 180
    
    		self.arrowHead.resetTransform()
    		self.arrowHead.rotate(arrow_theta)
    		self.arrowHead.setPos(vector[0], vector[1])
    		
    		if not isResult:
    			self.result_label.setText("<span style='font-size: 10pt; color :orange'>Weight<br/> </span>  <span style='font-size: 12pt;color: gray'>(%0.3f,%0.3f)</span> <br/><br/>  <span style='font-size: 10pt; color: orange'>Bias<br/></span><span style='font-size: 12pt;color:gray'>%0.3f</span>" % (weight_vector[0],weight_vector[1],weight_vector[2]))
    		else:
    			self.result_label.setText("<span style='font-size: 10pt; color :orange'>Weight<br/> </span>  <span style='font-size: 12pt;color: rgb(0,255,0)'>(%0.3f,%0.3f)</span> <br/><br/>  <span style='font-size: 10pt; color: orange'>Bias<br/></span><span style='font-size: 12pt;color:rgb(0,255,0)'>%0.3f</span>" % (weight_vector[0],weight_vector[1],weight_vector[2]))
    
    		
    	def highlightPoint(self, point, lastPoint):
    		
    		if lastPoint is not None:
    			lastPoint.setData(symbolPen = "w", symbol = lastPoint.getShape(), symbolBrush = lastPoint.getColor(), pen = lastPoint.getColor())
    			lastPoint.reassignData("w")
    			lastPoint.setData([lastPoint.xData[0]],[lastPoint.yData[0]])
    		
    		if point is not None:
    			point.setData(symbolPen = pg.mkPen((0,255,0), width=3), symbol = point.getShape(), symbolBrush = point.getColor(),pen = point.getColor())
    			point.reassignData(pg.mkPen((0,255,0), width=3))
    
    			point.setData([point.xData[0]],[point.yData[0]])
    			
    	def clickedRunAlgo(self):
    	
    		self.decision_boundary.setPen(pg.mkPen((0,80, 110), width = 2.5))
    		self.plot.addItem(self.decision_boundary)
    		
    		self.plot.addItem(self.supporting_vector)
    		self.plot.addItem(self.arrowHead)
    		self.thread.start()
    		
    		print("starting...")
    		
    	def btnDelClicked(self):
    		
    		if(not MainWindow.isDeleting):
    			MainWindow.isDeleting = True
    			self.btnDel.setText("Plot")
    			self.plot.removeItem(self.movingPoint)
    		else:
    			MainWindow.isDeleting = False
    			self.btnDel.setText("Delete")
    	
    	def btnClearAllClicked(self):
    		for list in self.allPoints:
    			for pt in list:
    				self.plot.removeItem(pt)
    		
    		self.allPoints.clear()
    		
    		self.plot.removeItem(self.supporting_vector);self.supporting_vector.setData([0,0],[0,0])
    
    		self.plot.removeItem(self.decision_boundary)
    		self.plot.removeItem(self.arrowHead)
    		self.decision_boundary.setPen(pg.mkPen((0,80, 110), width = 2.5))
    		self.result_label.setText("<span style='font-size: 10pt; color :orange'>Weight<br/> </span>  <span style='font-size: 12pt;color: gray'>(%0.3f,%0.3f)</span> <br/><br/>  <span style='font-size: 10pt; color: orange'>Bias<br/></span><span style='font-size: 12pt;color:gray'>%0.3f</span>" % (0,0,0))
    
    		self.updateLegend()
    		
    	def comboIndexChanged(self):
    		self.currentIndex = self.shape_combo.currentIndex()
    		self.movingPoint.setData(symbol = self.combo_icons[self.currentIndex], symbolBrush = self.point_colors[self.combo_icons[self.currentIndex]])
    		self.pointColorBtn.setStyleSheet("background-color: rgb" + str(self.point_colors[self.combo_icons[self.currentIndex]]))
    		
    		self.point_colors[self.combo_icons[self.currentIndex]]
    
    
    	def clickTestEvnet(self):
    		self.plot.setXRange(xAxisMin, xAxisMax, padding = 0)
    		self.plot.setYRange(yAxisMin, yAxisMax, padding = 0)
    
    	def mouseClicked(self, evt):
    		
    		if(self.isDeleting):
    			return
    	
    		pos = evt[0]
    		try:
    			point = DataPoint(self, self.combo_icons[self.currentIndex],self.point_colors[self.combo_icons[self.currentIndex]])
    			point.setZValue(2)
    			x = self.plot.getViewBox().mapSceneToView(pos.scenePos()).x()
    			y = self.plot.getViewBox().mapSceneToView(pos.scenePos()).y()
    			print("x, y", x, y)
    			point.setData([x],[y])
    			
    			isFound = False
    			
    			for pointList in self.allPoints:
    				if(pointList[0].getShape() == point.getShape()):
    					pointList.append(point)
    					isFound = True
    					
    			if(isFound == False):
    				if(len(self.allPoints) == self.maxNumberOfClass):
    					return
    				self.allPoints.append([point])
    			self.plot.addItem(point)
    
    		except:
    			print("error")
    		
    		self.updateLegend()
    			
    	
    	def updateLegend(self):
    		xMin = self.plot.viewRange()[0][0]
    		yMax = self.plot.viewRange()[1][1]
    
    		viewBox = self.plot.getViewBox()
    
    		for item in self.label_icons:
    			viewBox.removeItem(item.labelPoint)
    			viewBox.removeItem(item.labelText)
    
    		self.label_icons.clear()
    		i = 1
    		for pointList in self.allPoints:
    			
    			legendRow = LegendRow([10],[i * 20],symbol = pointList[0].getShape(), color = pointList[0].getColor())
    			legendRow.labelText.setText(str(len(pointList)))
    			legendRow.labelPoint.setParentItem(viewBox)
    			legendRow.labelText.setParentItem(viewBox)
    			self.label_icons.append(legendRow)
    			i = i + 1
    
    	def mouseMoved(self, evt):
    		if(MainWindow.isDeleting):
    			return
    		pos = evt[0]
    			
    		if self.plot.sceneBoundingRect().contains(pos):
    			
    			mousePoint = self.plot.vb.mapSceneToView(pos)
    			self.movingPoint.setData([mousePoint.x()],[mousePoint.y()])
    			self.plot.addItem(self.movingPoint)
    
    if __name__ == '__main__':
    
        app = QApplication(sys.argv)
        ex = MainWindow()
        
        if(sys.flags.interactive != 1) or not hasattr(QtCore, 'PYQT_VERSION'):
            app.exec_()
    	

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/

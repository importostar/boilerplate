---
title: matplolib_realtime_gui
date: 2020-05-07
---
Example Python program matplolib_realtime_gui.py
This program creates a PyQt GUI

## Modules

* import sys
* from PyQt5 import QtWidgets
* from matplo_realtime_ui import Ui_Form
* import matplotlib
* from PyQt5 import QtCore, QtWidgets
* from matplotlib.backends.backend_qt5agg import FigureCanvasQTAgg as FigureCanvas
* from matplotlib.figure import Figure
* import numpy 
* import random

## Classes

* class MyMplCanvas(FigureCanvas):
* class MyDynamicMplCanvas(MyMplCanvas):
* class Form(QtWidgets.QDialog):

## Methods

* 	def __init__(self, parent=None, width=5, height=2, dpi=100):
* 		def compute_initial_figure(self):
* 	def __init__(self, *args, **kwargs):
* 	def compute_initial_figure(self):
* 	def update_figure(self):
* 	def __init__(self, parent=None):
* 	def show_graph(self):

## Code

Example Python PyQt program :

    import sys
    from PyQt5 import QtWidgets
    #matplo_realtime_ui.pyの読み込み
    from matplo_realtime_ui import Ui_Form
    
    #以下7~12はpyqt上でmatlaboを動かすのに必要なライブラリ
    import matplotlib
    matplotlib.use('Qt5Agg')
    from PyQt5 import QtCore, QtWidgets
    from matplotlib.backends.backend_qt5agg import FigureCanvasQTAgg as FigureCanvas
    from matplotlib.figure import Figure
    import numpy 
    
    #ランダム関数を使うので
    import random
    
    #FigureCanvasはFigureCanvasQTAgg 10行目で定義
    class MyMplCanvas(FigureCanvas):
    	
    	def __init__(self, parent=None, width=5, height=2, dpi=100):
    		fig = Figure(figsize=(width, height), dpi=dpi)
    		self.axes = fig.add_subplot(111)
    
    		self.compute_initial_figure()
    		FigureCanvas.__init__(self, fig)
    		self.setParent(parent)
    		FigureCanvas.setSizePolicy(self, QtWidgets.QSizePolicy.Expanding,QtWidgets.QSizePolicy.Expanding)
    		FigureCanvas.updateGeometry(self)
    
    		def compute_initial_figure(self):
    			pass
    		
    #18行目から定義したクラスMyMplCanvasを継承
    class MyDynamicMplCanvas(MyMplCanvas):
    
    	def __init__(self, *args, **kwargs):
    		MyMplCanvas.__init__(self, *args, **kwargs)
    		#タイマーをセット
    		timer = QtCore.QTimer(self)
    		timer.timeout.connect(self.update_figure)
    		#100msごとに更新
    		timer.start(100)
    		#x軸の幅を定義
    		self.xlim = [0,100]
    		self.X= []
    		self.Y= []
    
    	def compute_initial_figure(self):
    		pass
    
    	def update_figure(self):
    		#値がXに100個以上格納されたら。1をX[0],X[1]に足すことでx軸の幅を一定にする
    		if len(self.X) > 100:
    			self.xlim[0] += 1
    			self.xlim[1] += 1
    		self.axes.cla()
    		#Yの値を格納
    		self.Y.append(random.random())
    		#Yに格納されている数をXに追加
    		self.X.append(len(self.Y))
    		self.axes.plot(self.X,self.Y)
    		#Y軸の描画範囲
    		self.axes.set_ylim(-1,2)
    		#X軸の描画範囲
    		self.axes.set_xlim(self.xlim[0], self.xlim[1])
    		self.draw()
    
    #widgetsの内容		
    class Form(QtWidgets.QDialog):
    	def __init__(self, parent=None):
    		super(Form, self).__init__(parent)
    		self.ui = Ui_Form()
    		self.ui.setupUi(self)
    		self.l = QtWidgets.QVBoxLayout(self.ui.widget)
    	#グラフ表示
    	def show_graph(self):
    		sc = MyDynamicMplCanvas(self.ui.widget, width=5, height=4, dpi=100)
    		self.l.addWidget(sc)
    
    if __name__ == '__main__':
    	app = QtWidgets.QApplication(sys.argv)
    	window = Form()
    	window.show()
    	sys.exit(app.exec_())
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/

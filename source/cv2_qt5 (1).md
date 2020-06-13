---
title: cv2_qt5 (1)
date: 2020-05-07
---
Example Python program cv2_qt5 (1).py
This program creates a PyQt GUI

## Modules

* import cv2
* import cv2.cv as cv
* import numpy as np
* import sys
* from PyQt5.QtCore import *
* from PyQt5.QtGui import *
* from PyQt5.QtWidgets import *
* 	import sys

## Classes

* class Pixmap(QGraphicsObject):
* class IplQImage(QImage):
* class VideoWidget(QWidget) :
* class MainView(QGraphicsView):

## Methods

* 	def __init__(self, pix):
* 	def paint(self, painter, option, widget):
* 	def boundingRect(self):
* 	def __init__(self,iplimage):
* 	def __init__(self, parent=None):
* 	def _build_image(self,rval, frame):
* 	def paintEvent(self, event):
* 	def queryFrame(self):
* 	def getSize(self):
* 	def __init__(self, parent=None):
* 	def queryFrame(self):

## Code

Example Python PyQt program :

    #coding: utf-8
    
    import cv2
    import cv2.cv as cv
    import numpy as np
    import sys
    
    from PyQt5.QtCore import *
    from PyQt5.QtGui import *
    from PyQt5.QtWidgets import *
    
    class Pixmap(QGraphicsObject):
    	def __init__(self, pix):
    		super(Pixmap, self).__init__()
    
    		self.p = QPixmap(pix)
    
    	def paint(self, painter, option, widget):
    		painter.drawPixmap(QPointF(), self.p)
    
    	def boundingRect(self):
    		return QRectF(QPointF(0, 0), QSizeF(self.p.size()))
    
    class IplQImage(QImage):
    	#Qtで使用できるimageにCVのキャプチャを変換
    	def __init__(self,iplimage):
    		# Rough-n-ready but it works dammit
    		alpha = np.zeros((iplimage.shape[0],iplimage.shape[1]), np.uint8)
    		# Zieht ein schwarzes Rechteck ueber das Bild
    		cv2.rectangle(alpha, (0, 0), (iplimage.shape[1],iplimage.shape[0]), cv.ScalarAll(255) ,-1)
    		rgba = np.zeros((iplimage.shape[0], iplimage.shape[1], 4), np.uint8)
    		cv2.mixChannels([iplimage, alpha],[rgba], [
    			0, 0, # rgba[0] -> bgr[2]
    			1, 1, # rgba[1] -> bgr[1]
    			2, 2, # rgba[2] -> bgr[0]
    			3, 3  # rgba[3] -> alpha[0]
    			])
    		self.__imagedata = rgba.tostring()
    		super(IplQImage,self).__init__(self.__imagedata, iplimage.shape[1], iplimage.shape[0], QImage.Format_RGB32)
    
    class VideoWidget(QWidget) :
    
    	def __init__(self, parent=None):
    		super(VideoWidget, self).__init__(parent)
                    self._capture = cv2.VideoCapture(0)
    		ret, frame = self._capture.read()
    
    		#キャプチャサイズを取得
    		self.width = np.size(frame, 1)
    		self.height = np.size(frame, 0)
    
    		#ウィンドウサイズ設定
    		self.setMinimumSize(self.width, self.height)
    		self.setMaximumSize(self.minimumSize())
    
    		self._frame = None
    		self.direction = None
    		self._image = self._build_image(ret, frame)
    
    
    	def _build_image(self,rval, frame):
    		if not rval:
    			self._frame = np.zeros((frame.shape[0], frame.shape[1]), np.uint8, frame.shape[2])
    		self._frame = frame
    		return IplQImage(self._frame)
    
    	def paintEvent(self, event):
    		painter = QPainter(self)
    		painter.drawImage(QPoint(0, 0), self._image)
    
    	#繰り返し処理
    	def queryFrame(self):
    		rval, frame = self._capture.read()
    		vis = frame.copy()
    
    		self._image = self._build_image(rval, vis)
    		self.update()
    
    	def getSize(self):
    		return self.width, self.height
    
    class MainView(QGraphicsView):
    	def __init__(self, parent=None):
    		super(QGraphicsView, self).__init__(parent)
    
    		#キャプチャした画像を背景に設定して、画像の大きさにウィンドウサイズを設定
    		self.widget = VideoWidget()
    		width, height = self.widget.getSize()
    		scene = QGraphicsScene(0, 0, width, height)
    		self.setScene(scene)
    		proxyWidget = QGraphicsProxyWidget()
    		proxyWidget.setWidget(self.widget) 
    		scene.addItem(proxyWidget)
    
    		self._timer = QTimer(self)
    		self._timer.timeout.connect(self.queryFrame)
    		self._timer.start(50)
    
    	def queryFrame(self):
    		self.widget.queryFrame()
    
    if __name__ == '__main__':
    	import sys
    
    	app = QApplication(sys.argv);
    
    	view = MainView()
    	view.show()
    
    	sys.exit(app.exec_())

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/

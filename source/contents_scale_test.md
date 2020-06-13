---
title: contents_scale_test
date: 2020-05-07
---
Example Python program contents_scale_test.py
This program creates a PyQt GUI

## Modules

* from PyQt5.QtGui import QPainter
* from PyQt5.QtCore import *
* from PyQt5.QtQuick import *
* from PyQt5.QtWidgets import *
* 	import sys

## Classes

* class Item(QQuickPaintedItem):
* class Window(QMainWindow):

## Methods

* 	def __init__(self, useBoundRect, parent=None):
* 	def getBoundRect(self):
* 	def paint(self, painter):
* 	def __init__(self, parent=None):
* 	def add_item(self, useBoundRect, x, y, w, h, ss, cw, ch, cs, col):

## Code

Example Python PyQt program :

    #!/usr/bin/env python3
    
    from PyQt5.QtGui import QPainter
    from PyQt5.QtCore import *
    from PyQt5.QtQuick import *
    from PyQt5.QtWidgets import *
    
    class Item(QQuickPaintedItem):
    	def __init__(self, useBoundRect, parent=None):
    		super().__init__(parent)
    		self._ubr = useBoundRect
    	
    	def getBoundRect(self):
    		if self._ubr:
    			return self.contentsBoundingRect()
    		else:
    			return QRectF(0, 0, self.width(), self.height())
    	
    	def paint(self, painter):
    		br = self.getBoundRect()
    		font = painter.font()
    		painter.drawText(br, Qt.TextWordWrap | Qt.AlignCenter, 'Hello, cruel world!')
    
    class Window(QMainWindow):
    	def __init__(self, parent=None):
    		super().__init__(parent)
    		self._win = QQuickWindow()
    		self._cont = QWidget.createWindowContainer(self._win)
    		self._items = []
    		self.setCentralWidget(self._cont)
    		self.resize(420, 400)
    
    	def add_item(self, useBoundRect, x, y, w, h, ss, cw, ch, cs, col):
    		root = self._win.contentItem()
    		it = Item(useBoundRect, root)
    		it.setX(x)
    		it.setY(y)
    		it.setScale(ss)
    		it.setWidth(w)
    		it.setHeight(h)
    		it.setContentsScale(cs)
    		it.setContentsSize(QSize(cw, ch))
    		it.setFillColor(col)
    		self._items.append(it)
    		return it
    
    if __name__ == '__main__':
    	import sys
    	app = QApplication(sys.argv)
    	win = Window()
    	win.show()
    	# First and second rows: painting uses contentsBoundingRect()
    	# First row: just use item's scale. Content is low-res, but scaled
    	#           BoRect,   x    y    w   h  scale cw  ch  cscale, color
    	win.add_item(True,   10,  10, 100, 50,   1,   -1, -1,   1, Qt.green)
    	win.add_item(True,  150,  20, 100, 50, 1.5,   -1, -1,   1, Qt.yellow)
    	win.add_item(True,  275,  10, 100, 50, 0.5,   -1, -1,   1, Qt.yellow)
    	# Second row: scale the contents instead of the item
    	#           BoRect,   x    y    w   h  scale cw  ch  cscale, color
    	win.add_item(True,  10,  100,   1,  1,   1,  100, 50,   1, Qt.red)
    	win.add_item(True,  125, 100,   1,  1,   1,  100, 50, 1.5, Qt.magenta)
    	win.add_item(True,  300, 100,   1,  1,   1,   50, 25, 0.5, Qt.magenta)
    
    	# Third and fourth rows: painting uses width() and height()
    	# Third row: scale the item, same result as before
    	win.add_item(False,  10, 210, 100, 50,   1,   -1, -1,   1, Qt.darkGreen)
    	win.add_item(False, 150, 220, 100, 50, 1.5,   -1, -1,   1, Qt.darkYellow)
    	win.add_item(False, 275, 220, 100, 50, 0.5,   -1, -1,   1, Qt.darkYellow)
    	# Fourth row: scale the content
    	win.add_item(False,  10, 300, 100, 50,   1,  100, 50,   1, Qt.darkRed)
    	win.add_item(False, 125, 300, 100, 50,   1,  100, 50, 1.5, Qt.darkMagenta)
    	win.add_item(False, 300, 300, 100, 50,   1,   50, 25, 0.5, Qt.darkMagenta)
    	#           BoRect,   x    y    w   h  scale cw  ch  cscale, color
    
    	sys.exit(app.exec_())
    
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/

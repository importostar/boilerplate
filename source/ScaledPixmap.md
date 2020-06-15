---
title: ScaledPixmap
date: 2020-05-07
---
Example Python program ScaledPixmap.py

## Modules

* from PyQt5.QtWidgets import QLabel
* from PyQt5.Qt import Qt, QSize
* from PyQt5.QtGui import QPixmap, QPainter
* from PyQt5 import QtCore

## Classes

* class ScaledPixmap(QLabel):

## Methods

* def getPixmap(self):
* def overscaleEnabled(self):
* def keepAspectRatioEnabled(self):
* def fitsToScreen(self, screenSize):
* def paintEvent(self, event):
* def setScaledPixmap(self, pixmap):
* def loadPixmapData(self, source):
* def loadPixmapData(self, pixmap):
* def setOverscaleEnabled(self, enabled):
* def setKeepAspectRatioEnabled(self, enabled):

## Code

Example Python PyQt program :

    from PyQt5.QtWidgets import QLabel
    from PyQt5.Qt import Qt, QSize
    from PyQt5.QtGui import QPixmap, QPainter
    from PyQt5 import QtCore
    
    
    class ScaledPixmap(QLabel):
        workPixmap = None
        originalSize = None
    
        keepAspectRatio = False
        overscalingEnabled = False
    
        loadFinished = QtCore.pyqtSignal()
    
        def getPixmap(self):
            return self.workPixmap
    
        def overscaleEnabled(self):
            return self.overscalingEnabled
    
        def keepAspectRatioEnabled(self):
            return self.keepAspectRatio
    
        def fitsToScreen(self, screenSize):
            return (screenSize.width() >= self.originalSize.width()) and (screenSize.height() >= self.originalSize.height())
    
        def paintEvent(self, event):
            painter = QPainter(self)
            if self.workPixmap is not None:
                centerPoint = QtCore.QPoint(0, 0)
                scaledSize = self.size() if self.overscaleEnabled() else (self.originalSize if self.fitsToScreen(self.size()) else self.size())
                scaledPixmap = self.workPixmap.scaled(scaledSize,
                                                      Qt.KeepAspectRatio if self.keepAspectRatio else Qt.IgnoreAspectRatio)
                centerPoint.setX((self.size().width() - scaledPixmap.width()) / 2)
                centerPoint.setY((self.size().height() - scaledPixmap.height()) / 2)
                painter.drawPixmap(centerPoint, scaledPixmap)
    
            super().paintEvent(event)
    
        @QtCore.pyqtSlot(QPixmap, name='setScaledPixmap')
        def setScaledPixmap(self, pixmap):
            self.workPixmap = pixmap
            self.originalSize = pixmap.size()
            self.update()
    
        @QtCore.pyqtSlot(str, name='loadPixmapData')
        def loadPixmapData(self, source):
            pixmap = QPixmap(source)
            if pixmap is not None:
                self.setScaledPixmap(pixmap)
    
        @QtCore.pyqtSlot(QPixmap, name='loadPixmapData')
        def loadPixmapData(self, pixmap):
            if pixmap is not None:
                self.setScaledPixmap(pixmap)
    
        @QtCore.pyqtSlot(int, name='setOverscaleEnabled')
        def setOverscaleEnabled(self, enabled):
            self.overscalingEnabled = enabled
    
        @QtCore.pyqtSlot(int, name='setKeepAspectRatioEnabled')
        def setKeepAspectRatioEnabled(self, enabled):
            self.keepAspectRatio = enabled
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/

---
title: redox
date: 2020-05-07
---
Example Python program redox.py
This program creates a PyQt GUI
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import sys
* import os
* from PyQt5.QtCore import *
* from PyQt5.QtGui import *
* from PyQt5.QtWidgets import *
* from htmapui import HtMapGui
* #from qimage import QImageWidget
* import sys

## Classes

* class QImageWidget(QWidget):
* class MapDisplay(QObject):

## Methods

* def __init__(self, pixmap, width, height, parent=None):
* def set_pixmap(self, pixmap):
* def paintEvent(self, event):
* def hasHeightForWidth(self):
* def heightForWidth(self, w):
* def __init__(self):
* def initUI(self):
* def getImageDir_hard(self):
* def updatespinbox(self):
* def decreaseimageindex(self):
* def increaseimageindex(self):
* def addImage2(self):
* def addImage(self):
* def setValueZoomStepspinBox(self, z):
* def setValueZoomStepSlider(self, z):
* def setValue(self, v):
* def setValueImageIndexspinBox(self, z):
* def setValueImageIndexSlider(self, z):
* def setImageIndexStepValue(self):

## Code

Example Python PyQt program :

    #!/usr/local/bin/python36
    
    
    import sys
    import os
    from PyQt5.QtCore import *
    from PyQt5.QtGui import *
    from PyQt5.QtWidgets import *
    from htmapui import HtMapGui
    
    #from qimage import QImageWidget
    
    class QImageWidget(QWidget):
        def __init__(self, pixmap, width, height, parent=None):
            super().__init__(parent)
            #self.pixmap = QtGui.QPixmap('201503.20150619.200707736.246017.jpg')
            self.pixmap = None
            self.height_per_width = None
            self.width = width
            self.height = height
            self.set_pixmap(pixmap)
    
    
        def set_pixmap(self, pixmap):
            self.pixmap = pixmap
            self.height_per_width = self.pixmap.height() / self.pixmap.width()
    
        def paintEvent(self, event):
            painter = QPainter(self)
    
            '''
            current_height_per_width = self.height() / self.width()
    
            if current_height_per_width > self.height_per_width:
                width = self.width()
                height = width * self.height_per_width
                top = (self.height() - height) / 2
                left = 0
            else:
                height = self.height()
                width = height / self.height_per_width
                left = (self.width() - width) / 2
                top = 0
            '''
            left = 0
            top = 0
            #target = QRect(left, top, width, height)
            target = QRect(left, top, self.width, self.height)
    
            painter.drawPixmap(target, self.pixmap, self.pixmap.rect())
    
        def hasHeightForWidth(self):
            return True
    
        def heightForWidth(self, w):
            return w * self.height_per_width
            
    class MapDisplay(QObject):
        def __init__(self):
            super().__init__()
            self.initUI()
        
        def initUI(self):
            self.w = HtMapGui()   
            self.image=QLabel()
            self.w.scrollArea_3.setWidget(self.image)
            #self.w.verticalLayout_13.addWidget(self.image) 
            self.imagelist = []
            self.imageindex = 1
            self.ZoomStepValue = 50        
            self.w.fwd.clicked.connect(self.increaseimageindex)
            self.w.fwd.clicked.connect(self.updatespinbox)
            #self.w.scrollArea_3.setHorizontalScrollBarPolicy(Qt.ScrollBarAlwaysOn)
            #self.w.scrollArea_3.setVerticalScrollBarPolicy(Qt.ScrollBarAlwaysOn)
            #self.w.fwd.clicked.connect(self.addImage)        
            self.w.rwd.clicked.connect(self.decreaseimageindex)
            #self.w.rwd.clicked.connect(self.addImage)
            # ZOOM
            self.w.ZoomStepSlider.valueChanged.connect(self.setValueZoomStepspinBox)
            self.w.ZoomStepSlider.valueChanged.connect(self.addImage)
            #self.w.ZoomStepSlider.valueChanged.connect(self.addImage)
            self.w.ZoomStepspinBox.valueChanged.connect(self.setValueZoomStepSlider)
            #self.w.ZoomStepspinBox.valueChanged.connect(self.printFunction)
            self.w.ZoomStepSlider.valueChanged.connect(self.setValue)
            self.w.ZoomStepspinBox.valueChanged.connect(self.setValue)
            # Image Index
            self.w.ImageIndexSlider.valueChanged.connect(self.setValueImageIndexspinBox)
            #self.w.ImageIndexSlider.valueChanged.connect(self.printFunction)
            self.w.ImageIndexspinBox.valueChanged.connect(self.setValueImageIndexSlider)
            self.w.ImageStepspinBox.valueChanged.connect(self.setImageIndexStepValue)
            #self.w.ImageIndexSlider.valueChanged.connect(self.addImage)
            self.w.ImageIndexSlider.valueChanged.connect(self.addImage)
            # hardcoded image file and metadata        
            self.getImageDir_hard()
            
            self.w.ZoomStepSlider.setMinimum(1)
            
            self.w.show()
    
        def getImageDir_hard(self):
            cwd = os.getcwd() #os.path.realpath(os.path.abspath(__file__))
            self.dirname = os.path.join(cwd,'images')
            if self.dirname:
                self.imagelist = os.listdir(self.dirname)
                self.w.ImageIndexspinBox.setMaximum(len(self.imagelist) - 1)
                self.w.ImageIndexSlider.setMaximum(len(self.imagelist) - 1)
    
        def updatespinbox(self):
             self.w.ImageIndexspinBox.setValue(self.imageindex)
             self.w.ImageIndexSlider.update()
             self.w.ImageIndexspinBox.update()
             print('fwd pressed')
        
        def decreaseimageindex(self):
            self.imageindex=self.imageindex-self.w.ImageStepspinBox.value()
            self.w.ImageIndexSlider.setValue(self.imageindex)
            self.w.ImageIndexspinBox.setValue(self.imageindex)
        
        def increaseimageindex(self):
            self.imageindex = self.imageindex+self.w.ImageStepspinBox.value()
            self.w.ImageIndexSlider.setValue(self.imageindex)
            self.w.ImageIndexspinBox.setValue(self.imageindex)
    
    
        def addImage2(self):
            #self.w.verticalLayout_13.removeWidget(self.image)
            self.image.setParent(None)
            self.pixmap = QPixmap(os.path.join(self.dirname, self.imagelist[self.imageindex]))
            width=self.pixmap.width()*(self.ZoomStepValue/100.)
            height=self.pixmap.height()*(self.ZoomStepValue/100.)
            #self.pixmap = self.pixmap.scaled(width, height, Qt.KeepAspectRatio)
            self.image = QImageWidget(self.pixmap, width, height)
            self.w.verticalLayout_13.addWidget(self.image)
    
        
        def addImage(self):
            #self.w.image.clear()
            #self.w.image.setGeometry(QRect(0, 0, 1360, 1024))
             
            if any(self.imagelist) is not None:            
                self.pixmap = QPixmap(os.path.join(self.dirname, self.imagelist[self.imageindex]))
                print('orig size:', self.pixmap.width(), self.pixmap.height())
                width=self.pixmap.width()*(self.ZoomStepValue/100.)
                height=self.pixmap.height()*(self.ZoomStepValue/100.)
                self.pixmap = self.pixmap.scaled(width, height, Qt.KeepAspectRatio)
                print('height', self.image.height())
                print('width', self.image.width())
                print('heightMM', self.image.heightMM())
                print('widthMM', self.image.widthMM())
                #self.w.image.clear()         
                self.image.setGeometry(QRect(0, 0, width, height))
                #self.w.image.setPixmap(self.pixmap)
                self.image.setPixmap(self.pixmap)
                #self.image.setPixmap(self.pixmap.scaled(
                #                    self.image.size(),
                #                    Qt.KeepAspectRatio,
                #                    Qt.SmoothTransformation))
            else:
                print('both image path not be set')
                print(' --- ')
    
    
    
        def setValueZoomStepspinBox(self, z):
            self.ZoomStepValue = int(z)
            #self.w.ZoomStepspinBox.setRange(1, 100)
            self.w.ZoomStepspinBox.setSingleStep(1)
            self.w.ZoomStepspinBox.setValue(self.ZoomStepValue)
            self.addImage
    
        def setValueZoomStepSlider(self, z):
            self.ZoomStepValue = int(z)
            
            #self.w.ZoomStepSlider.setMaximum(100)
            self.w.ZoomStepSlider.setValue(self.ZoomStepValue)
    
        def setValue(self, v):
            self.Value = v
        
        def setValueImageIndexspinBox(self, z):
            self.imageindex = int(z)
            self.w.ImageIndexspinBox.setSingleStep(self.w.ImageStepspinBox.value())
            self.w.ImageIndexspinBox.setValue(self.imageindex)
        
        def setValueImageIndexSlider(self, z):
            self.imageindex = int(z)
            self.w.ImageIndexSlider.setSingleStep(self.w.ImageStepspinBox.value())
            self.w.ImageIndexSlider.setValue(self.imageindex)
        
        def setImageIndexStepValue(self):
            self.w.ImageIndexspinBox.setSingleStep(self.w.ImageStepspinBox.value())
            self.w.ImageIndexSlider.setSingleStep(self.w.ImageStepspinBox.value())
    
        
            
    if __name__ == "__main__":
        import sys
        app = QApplication(sys.argv)
        app.processEvents()
        p = MapDisplay()
        sys.exit(app.exec_())
    
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/

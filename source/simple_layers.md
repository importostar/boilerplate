---
title: simple_layers
date: 2020-05-07
---
Example Python program simple_layers.py
This program creates a PyQt GUI

## Modules

* import sys
* from PyQt5.QtCore import *
* from PyQt5.QtGui import *
* from PyQt5.QtWidgets import *

## Classes

* class LayerWidget(QWidget):
* class LayerScene(QGraphicsScene):
* class AnimatedGIF(QGraphicsPixmapItem):

## Methods

* def __init__(self, parent=None):
* def resizeEvent(self, event):
* def __init__(self, parent=None):
* def __init__(self, filename, parent=None):
* def nextFrame(self, n):
* def start(self):
* def main():

## Code

Example Python PyQt program :

    # A simple example to implement a layer feature, it tests:
    # -- Layers
    # -- .gif load and aniamiton
    # -- Zooming
    #
    # All if this should be done using the QGraphicsView Framework
    
    import sys
    from PyQt5.QtCore import *
    from PyQt5.QtGui import *
    from PyQt5.QtWidgets import *
    
    # TODO, this is now segfaulting because of update to PyQt5, fix it
    
    
    class LayerWidget(QWidget):
    
        def __init__(self, parent=None):
            super(LayerWidget, self).__init__(parent)
    
            # Some Varibales
            self.scale = 2
            self.viewSize = QSize()         # Size we want for the view at all times
    
            # Get the scene
            self.scene = LayerScene(self)
    
            # Set the view
            self.view = QGraphicsView(self)
            self.view.setScene(self.scene)              # Doesn't segfault if a scene is not set
            self.view.setFrameShape(QFrame.NoFrame)
            self.view.scale(self.scale, self.scale)
    
            self.viewSize = self.scene.sceneRect().toRect().size() * self.scale
    
            # Other
            self.setWindowTitle('Simple Layers Test (w/ Animation)')
            self.resize(self.viewSize)
    
    
        def resizeEvent(self, event):
            # Try to keep the view in the center of the window at all times
            widgetSize = self.size()
            viewSize = self.viewSize
    
            # Check the sizes
            widgetWidthSmaller = widgetSize.width() < viewSize.width()
            widgetHeightSmaller = widgetSize.height() < viewSize.height()
            if widgetWidthSmaller or widgetHeightSmaller:
                # too small, resize the view
    
                # Make the new sized view
                newSize = QSize()
                newSize.setWidth(widgetSize.width() if widgetWidthSmaller else viewSize.width())
                newSize.setHeight(widgetSize.height() if widgetHeightSmaller else viewSize.height())
    
                newLoc = QPoint()
                newLoc.setX(0 if widgetWidthSmaller else self.view.pos().x())
                newLoc.setY(0 if widgetHeightSmaller else self.view.pos().y())
    
                # Change the minimum size and resize the view
                self.view.resize(newSize)
                self.view.move(newLoc)
            else:
                # No scrolly-bars
                self.view.resize(self.viewSize)
    
                # Keep it centered
                viewRect = self.view.rect()
                viewRect.moveCenter(self.rect().center())
                self.view.move(viewRect.topLeft())
    
    
    
    
    class LayerScene(QGraphicsScene):
        # Represents a "frame," with multiple layers  
    
        def __init__(self, parent=None):
            super(LayerScene, self).__init__(parent)
    
            self.layer = []
    
            # Hard code in some images
            self.layer.append(QGraphicsPixmapItem(QPixmap.fromImage(QImage('orange_glow.png'))))
            self.layer.append(AnimatedGIF('blue_spirit.gif'))
    
            self.layer[1].moveBy(50, 50)
    
            self.addItem(self.layer[0])
            self.addItem(self.layer[1])
            
            self.layer[1].start()
    
    
    
    
    class AnimatedGIF(QGraphicsPixmapItem):
        # A small test of an animated gif playing in a graphics scene
        
        def __init__(self, filename, parent=None):
            super(AnimatedGIF, self).__init__(parent)
    
            self.gif = QMovie(filename)
            self.gif.frameChanged[int].connect(self.nextFrame)
    
    
        @pyqtSlot(int)
        def nextFrame(self, n):
            self.setPixmap(self.gif.currentPixmap())
    
    
        def start(self):
            self.gif.start()
    
    
    
    def main():
        app = QApplication(sys.argv)
        lw = LayerWidget()
        lw.show()
    
        sys.exit(app.exec_())
    
    
    main()
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/

---
title: imager
date: 2020-05-07
---
Example Python program imager.py
This program creates a PyQt GUI

## Modules

* import sys
* from mainwindow import *
* from PyQt5 import Qt, QtCore, QtGui, QtWidgets
* from PyQt5.QtWidgets import QFileDialog
* from Boundaries import BoundariesOperation

## Classes

* class MyWin(QtWidgets.QMainWindow):

## Methods

* def __init__(self, parent=None):
* def loadImage(self):
* def getBoundaries(self):

## Code

Example Python PyQt program :

    import sys
    # Импортируем наш интерфейс из файла
    from mainwindow import *
    from PyQt5 import Qt, QtCore, QtGui, QtWidgets
    from PyQt5.QtWidgets import QFileDialog
    from Boundaries import BoundariesOperation
    
    
    class MyWin(QtWidgets.QMainWindow):
        def __init__(self, parent=None):
            QtWidgets.QWidget.__init__(self, parent)
            self.ui = Ui_MainWindow()
            self.ui.setupUi(self)
    
            # Здесь прописываем событие нажатия на кнопку
            self.ui.loadButton.clicked.connect(self.loadImage)
            self.ui.boundariesButton.clicked.connect(self.getBoundaries)
            self.ui.keepRatio.stateChanged.connect(self.ui.label.setKeepAspectRatioEnabled)
            self.ui.keepRatio.stateChanged.connect(self.ui.label_2.setKeepAspectRatioEnabled)
            self.ui.originalSize.stateChanged.connect(self.ui.label.setOverscaleEnabled)
            self.ui.originalSize.stateChanged.connect(self.ui.label_2.setOverscaleEnabled)
    
        # Пока пустая функция которая выполняется
        # при нажатии на кнопку
        def loadImage(self):
            inputImagePath = QFileDialog.getOpenFileName(self, 'Open image...', '/home')[0]
            inputPixmap = Qt.QPixmap(inputImagePath)
            self.ui.label.loadPixmapData(inputPixmap)
        
        def getBoundaries(self):
            if self.ui.label.pixmap():
                self.ui.label_2.setPixmap(BoundariesOperation.Execute(self.ui.label.pixmap()))
            
    
    if __name__ == "__main__":
        app = QtWidgets.QApplication(sys.argv)
        myapp = MyWin()
        myapp.show()
        sys.exit(app.exec_())
    
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/

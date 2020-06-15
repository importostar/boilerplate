---
title: pyqt5_5
date: 2020-05-07
---
Example Python program pyqt5_5.py
This program creates a PyQt GUI

## Modules

* from PyQt5.QtWidgets import (QApplication, QWidget, QComboBox, QDialog,
* from PyQt5.QtGui import (QIcon, QPixmap, QBrush, QPen, QColor)
* from PyQt5 import QtCore
* import sys
* import os
* import re

## Classes

* class MainWindow(QWidget):

## Methods

* def __init__(self,parent=None):

## Code

Example Python PyQt program :

    #!/usr/bin/env python
    from PyQt5.QtWidgets import (QApplication, QWidget, QComboBox, QDialog,
            QDialogButtonBox, QFormLayout, QGridLayout, QGroupBox, QHBoxLayout,
            QLabel, QLineEdit, QMenu, QMenuBar, QPushButton, QSpinBox, QTextEdit,
            QVBoxLayout, QGraphicsView, QGraphicsScene, QGraphicsItem, QGraphicsPixmapItem)
    from PyQt5.QtGui import (QIcon, QPixmap, QBrush, QPen, QColor)
    from PyQt5 import QtCore
    
    import sys
    import os
    import re
    
    
    class MainWindow(QWidget):
    
        def __init__(self,parent=None):
            #super() でスーパークラスのインスタンスメソッドを呼び出す
            super(MainWindow, self).__init__(parent)
    
            path = os.path.join(os.path.dirname(sys.modules[__name__].__file__), 'ico.png')
    
            view = QGraphicsView()
            scene = QGraphicsScene()
    
            item = QGraphicsPixmapItem(QPixmap(path))
    　　　　　#画像の位置調整
            item.setOffset (10, 10)
            scene.addItem(item)
    
    　　　　　#円をいっぱい描く。20×20
            for i in range(0,200,10):
                for j in range(0,200,10):
                    #QPenの設定
                    pen = QPen(QtCore.Qt.green, 1, QtCore.Qt.SolidLine, QtCore.Qt.RoundCap, QtCore.Qt.RoundJoin)
                    #QBrushの設定
                    brush = QBrush(QColor(255, 0, 0, 127),QtCore.Qt.Dense1Pattern)
                    scene.addEllipse(i,j,10,10,pen,brush)
    
            view.setScene(scene)
    
            mainLayout = QVBoxLayout()
            mainLayout.addWidget(view)
    
            self.setLayout(mainLayout)
            #windowのタイトル変更
            self.setWindowTitle("Test App5")
    
    if __name__ == '__main__':
        app = QApplication(sys.argv)
        path = os.path.join(os.path.dirname(sys.modules[__name__].__file__), 'ico.png')
        app.setWindowIcon(QIcon(path))
        P = MainWindow()
        P.show()
        sys.exit(app.exec_())

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/

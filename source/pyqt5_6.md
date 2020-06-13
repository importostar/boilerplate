---
title: pyqt5_6
date: 2020-05-07
---
Example Python program pyqt5_6.py
This program creates a PyQt GUI

## Modules

* from PyQt5.QtWidgets import (QApplication, QWidget, QComboBox, QDialog,
* from PyQt5.QtGui import (QIcon, QPixmap, QBrush, QPen, QColor)
* from PyQt5 import QtCore
* from PyQt5.QtCore import (QLineF, QPointF, QRectF, Qt)
* import sys
* import os
* import re

## Classes

* class Test_graphics(QGraphicsItem):
* class MainWindow(QWidget):

## Methods

* def __init__(self):
* def paint(self, painter, option, widget):
* def boundingRect(self):
* def redraw(self):
* def __init__(self,parent=None):
* def mousePressEvent(self, event):

## Code

Example Python PyQt program :

    #!/usr/bin/env python
    from PyQt5.QtWidgets import (QApplication, QWidget, QComboBox, QDialog,
            QDialogButtonBox, QFormLayout, QGridLayout, QGroupBox, QHBoxLayout,
            QLabel, QLineEdit, QMenu, QMenuBar, QPushButton, QSpinBox, QTextEdit,
            QVBoxLayout, QGraphicsView, QGraphicsScene, QGraphicsItem, QGraphicsPixmapItem)
    from PyQt5.QtGui import (QIcon, QPixmap, QBrush, QPen, QColor)
    from PyQt5 import QtCore
    from PyQt5.QtCore import (QLineF, QPointF, QRectF, Qt)
    
    import sys
    import os
    import re
    
    
    class Test_graphics(QGraphicsItem):
        def __init__(self):
            super(Test_graphics, self).__init__()
            self.time = 0
            self.a = 1
    
        def paint(self, painter, option, widget):
            painter.setPen(Qt.black)
            i = self.time
            painter.drawEllipse(i, i, 10, 10)
    　　　　　　　　#下の関数を入れないとうまく表示が更新されない。
        def boundingRect(self):
            return QRectF(0,0,400,400)
    
        def redraw(self):
            if self.time == 0:
                self.a = 1
            elif self.time >= 390:
                self.a = -1
            else:
                pass
            x = self.time + 10*self.a
            self.time = x
            self.update()
    
    class MainWindow(QWidget):
    
        def __init__(self,parent=None):
            super(MainWindow, self).__init__(parent)
            path = os.path.join(os.path.dirname(sys.modules[__name__].__file__), 'ico.png')
            view = QGraphicsView()
            scene = QGraphicsScene()
            self.item = Test_graphics()
            view.setSceneRect(0, 0, 400, 400);
            scene.addItem(self.item)
            view.setScene(scene)
            mainLayout = QVBoxLayout()
            mainLayout.addWidget(view)
            self.setLayout(mainLayout)
            #windowのタイトル変更
            self.setWindowTitle("Test App6")
    
        def mousePressEvent(self, event):
            self.item.redraw()
            super(MainWindow, self).mousePressEvent(event)
    
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

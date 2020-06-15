---
title: pyqt5_7
date: 2020-05-07
---
Example Python program pyqt5_7.py
This program creates a PyQt GUI

## Modules

* from PyQt5.QtWidgets import (QApplication, QWidget, QComboBox, QDialog,
* from PyQt5.QtGui import (QIcon, QPixmap, QBrush, QPen, QColor)
* from PyQt5 import QtCore
* from PyQt5.QtCore import (QLineF, QPointF, QRectF, Qt, QTimer)
* from PIL import Image, ImageDraw
* from glob import glob
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
* def time_Event(self):
* def make_movie(self):

## Code

Example Python PyQt program :

    #!/usr/bin/env python
    from PyQt5.QtWidgets import (QApplication, QWidget, QComboBox, QDialog,
            QDialogButtonBox, QFormLayout, QGridLayout, QGroupBox, QHBoxLayout,
            QLabel, QLineEdit, QMenu, QMenuBar, QPushButton, QSpinBox, QTextEdit,
            QVBoxLayout, QGraphicsView, QGraphicsScene, QGraphicsItem, QGraphicsPixmapItem)
    from PyQt5.QtGui import (QIcon, QPixmap, QBrush, QPen, QColor)
    from PyQt5 import QtCore
    from PyQt5.QtCore import (QLineF, QPointF, QRectF, Qt, QTimer)
    
    from PIL import Image, ImageDraw
    
    from glob import glob
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
    
            self.movieButton = QPushButton("&movie")
            self.movieButton.clicked.connect(self.make_movie)
            buttonLayout = QVBoxLayout()
            buttonLayout.addWidget(self.movieButton)
    
            path = os.path.join(os.path.dirname(sys.modules[__name__].__file__), 'ico.png')
            self.view = QGraphicsView()
            scene = QGraphicsScene()
            self.item = Test_graphics()
            self.view.setSceneRect(0, 0, 400, 400);
            item = QGraphicsPixmapItem(QPixmap(path))
            item.setOffset (110, 110)
            scene.addItem(item)
    
            scene.addItem(self.item)
            self.view.setScene(scene)
            mainLayout = QVBoxLayout()
            mainLayout.addWidget(self.view)
            mainLayout.addLayout(buttonLayout)
            self.setLayout(mainLayout)
            #windowのタイトル変更
            self.setWindowTitle("Test App7")
            self.plot_times = 0
            self.timer = QTimer(self)
            self.timer.timeout.connect(self.time_Event)
            self.timer.start(100)
    
            if os.path.isdir("./png") == False :
                os.mkdir("./png")
            else:
                pass
    
        def time_Event(self):
            self.item.redraw()
            self.plot_times = self.plot_times + 1
            if self.plot_times >= 10000 :
                plot_times_str = str(self.plot_times)
            elif self.plot_times >= 1000 :
                plot_times_str = "0" + str(self.plot_times)
            elif self.plot_times >= 100 :
                plot_times_str = "00" + str(self.plot_times)
            elif self.plot_times >= 10 :
                plot_times_str = "000" + str(self.plot_times)
            else :
                plot_times_str = "0000" + str(self.plot_times)
    
            self.view.grab().save("png/test_" + plot_times_str +".png")
    
        def make_movie(self):
            self.timer.stop()
            images = []
            file_num= glob("./png/**.png")
    
            file_num.sort()
    
            for i in range(0, len(file_num), 1):
                im =Image.open(file_num[i], 'r')
                fp = im.copy()
                im.close()
                images.append(fp)
    
            #duraton uints is micro seconds
            images[0].save("image.gif",
                   save_all=True, append_images=images[1:], optimize=False, duration=100, loop=0)
    
            for i in range(0, len(file_num), 1):
                os.remove(file_num[i])
            self.plot_times = 0
    
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

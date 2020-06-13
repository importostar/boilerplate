---
title: pyqt5_11_main
date: 2020-05-07
---
Example Python program pyqt5_11_main.py
This program creates a PyQt GUI

## Modules

* from PyQt5.QtWidgets import (QApplication, QWidget, QComboBox, QDialog,
* from PyQt5.QtGui import (QIcon, QPixmap, QBrush, QPen, QColor)
* from PyQt5 import (QtCore , QtGui)
* from PyQt5.QtCore import (QLineF, QPointF, QRectF, Qt, QTimer)
* from PIL import Image, ImageDraw
* from glob import glob
* import sys
* import os
* import re
* import cv2
* import subprocess

## Classes

* class Test_graphics(QGraphicsItem):
* class MainWindow(QWidget):

## Methods

* def __init__(self):
* def paint(self, painter, option, widget):
* def boundingRect(self):
* def redraw(self):
* def bar_move(self,input_x):
* def ball_move(self):
* def collision_bar(self):
* def collision_block(self):
* def __init__(self,parent=None):
* def time_Event(self):
* def keyPressEvent(self, e):

## Code

Example Python PyQt program :

    #!/usr/bin/env python
    from PyQt5.QtWidgets import (QApplication, QWidget, QComboBox, QDialog,
            QDialogButtonBox, QFormLayout, QGridLayout, QGroupBox, QHBoxLayout,
            QLabel, QLineEdit, QMenu, QMenuBar, QPushButton, QSpinBox, QTextEdit,
            QVBoxLayout, QGraphicsView, QGraphicsScene, QGraphicsItem, QGraphicsPixmapItem, QGraphicsTextItem)
    from PyQt5.QtGui import (QIcon, QPixmap, QBrush, QPen, QColor)
    from PyQt5 import (QtCore , QtGui)
    from PyQt5.QtCore import (QLineF, QPointF, QRectF, Qt, QTimer)
    from PIL import Image, ImageDraw
    from glob import glob
    import sys
    import os
    import re
    import cv2
    import subprocess
    
    class Test_graphics(QGraphicsItem):
        def __init__(self):
            super(Test_graphics, self).__init__()
            self.ball_start = 0
            self.x = 195
            self.y = 368
            self.a = 1
            self.b = -1
            self.bar_x = 175
            self.block = [[1 for i in range(8)] for j in range(4)]
            self.point = 0
            self.game_over = 0
            self.sound = os.path.join(os.path.dirname(sys.modules[__name__].__file__), "cannon_sound.py")
    
        def paint(self, painter, option, widget):
            #draw ball
            painter.setPen(Qt.black)
            painter.setBrush(Qt.white)
            painter.drawEllipse(self.x, self.y, 10, 10)
            #draw block
            painter.setPen(Qt.white)
            pen = [[255,0,0,255],[255,255,0,255],[0,255,0,255],[0,0,255,255]]
    
            for i in range(0,4,1):
                for j in range(0,8,1):
                    if self.block[i][j] == 1:
                        r = pen[i][0]
                        g = pen[i][1]
                        b = pen[i][2]
                        a = pen[i][3]
                        painter.setPen(Qt.white)
                        painter.setBrush(QColor(r,g,b,a))
                        painter.drawRect(50*j,20*i, 50, 20)
                        painter.setPen(Qt.white)
                        painter.setFont(QtGui.QFont("System" , 12, QtGui.QFont.Normal, False))
                        painter.drawText(QtCore.QRect(50*j,20*i, 50, 20) ,Qt.AlignCenter ,"10")
            #draw bar
            painter.setPen(Qt.red)
            painter.setBrush(Qt.white)
            painter.drawRect(self.bar_x, 379, 50, 10)
    
            if self.game_over == 1:
                painter.setPen(Qt.red)
                painter.setFont(QtGui.QFont("System" , 60, QtGui.QFont.Bold, False))
                painter.drawText(QtCore.QRect(0,0,400,400) ,Qt.AlignCenter ,"GAME OVER")
    
        def boundingRect(self):
            return QRectF(0,0,400,400)
    
        def redraw(self):
            if self.ball_start == 0:
                pass
            elif self.ball_start == 1:
                self.x = self.x + 10*self.a
                self.y = self.y + 10*self.b
                if self.x <= 0:
                    self.a = 1
                elif self.x >= 390:
                    self.a = -1
                else:
                    pass
                if self.y <= 0:
                    self.b = 1
                elif self.y >= 390:
                    #self.b = -1
                    self.game_over = 1
                    self.ball_start == 0
    
                else:
                    pass
                self.collision_bar()
                self.collision_block()
                self.update()
            elif self.ball_start == 2:
                pass
            return self.point
        def bar_move(self,input_x):
            if self.bar_x + input_x < -5:
                pass
            elif self.bar_x + input_x > 355:
                pass
            else:
                self.bar_x = self.bar_x + input_x
                if self.ball_start == 0:
                    self.x = self.x + input_x
            self.update()
    
        def ball_move(self):
            if self.ball_start == 0:
                self.ball_start = 1
            elif self.ball_start == 1:
                self.ball_start = 2
            elif self.ball_start == 2:
                self.ball_start = 1
            self.update()
    
        def collision_bar(self):
            r1 = (self.x - self.bar_x)**2 + (self.y - 359)**2
            r2 = (self.x - (self.bar_x+50))**2 + (self.y - 359)**2
            if ((self.y >= 359 and self.y <=385) and (self.bar_x <= self.x and self.bar_x +50 >= self.x)):
                self.b = -1
            elif (self.y >= 359 and self.y <=375) and (100 >= r1 or 100 >= r2):
                self.b = -1
    
        def collision_block(self):
            for i in range(0,4,1):
                for j in range(0,8,1):
                    if self.block[i][j]== 0:
                        pass
                    elif self.x > 50*j and self.x < 50*(j+1) and self.y > 20*i and self.y < 20*(i+1) :
                        self.block[i][j]= 0
                        subprocess.Popen(self.sound )
                        self.point = self.point + 10
                        if self.x > 50*j and self.x < 50*(j+1):
                            if self.b == 1:
                                self.b = -1
                            elif self.b == -1:
                                self.b = 1
                        elif self.y > 20*i and self.y < 20*(i+1):
                            if self.a == 1:
                                self.a = -1
                            elif self.a == -1:
                                self.a = 1
    
    class MainWindow(QWidget):
        def __init__(self,parent=None):
            super(MainWindow, self).__init__(parent)
            path = os.path.join(os.path.dirname(sys.modules[__name__].__file__), 'ico.png')
            self.view = QGraphicsView()
            scene = QGraphicsScene()
            self.item = Test_graphics()
            self.view.setSceneRect(0, 0, 400, 400);
            item = QGraphicsPixmapItem(QPixmap(path))
            item.setOffset (110, 110)
            self.text = QGraphicsTextItem("")
            self.text.setFont( QtGui.QFont( 'System Black', 30 ) )
            self.text.setTransform( QtGui.QTransform().translate( 250, 330))
            scene.addItem(item)
            scene.addItem(self.text)
            scene.addItem(self.item)
            self.view.setScene(scene)
            mainLayout = QVBoxLayout()
            mainLayout.addWidget(self.view)
            self.setLayout(mainLayout)
            self.setWindowTitle("Test App10")
            self.plot_times = 0
            self.timer = QTimer(self)
            self.timer.timeout.connect(self.time_Event)
            self.timer.start(100)
            if os.path.isdir("./png") == False :
                os.mkdir("./png")
            else:
                pass
    
        def time_Event(self):
            point = self.item.redraw()
            if point >= 100 :
                point = str(point) + "Point"
            elif point >= 10 :
                point = "0" + str(point) + "Point"
            else :
                point = "00" + str(point) + "Point"
            self.text.setPlainText(str(point))
    
        def keyPressEvent(self, e):
            pressed = e.key()
            if e.key() == Qt.Key_H: # 左
                self.item.bar_move(-10)
            elif e.key() == Qt.Key_L: # 右
                self.item.bar_move(10)
            elif e.key() == 16777220:
                self.item.ball_move()
    
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

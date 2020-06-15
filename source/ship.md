---
title: ship
date: 2020-05-07
---
Example Python program ship.py
This program creates a PyQt GUI

## Modules

* import sys
* from PyQt5 import QtWidgets
* from PyQt5 import QtCore
* from PyQt5 import QtGui
* import time
* import random
* import math

## Classes

* class SectionCon():
* class Missile():
* class Ship():
* class Form(QtWidgets.QWidget):

## Methods

* def __init__(self):
* def add(self, missile):
* def remove(self):
* def __init__(self, x, y, th, v):
* def draw(self, qp, sec_num):
* def __init__(self):
* def move_left(self):
* def move_right(self):
* def move_up(self):
* def move_down(self):
* def draw(self, qp):
* def __init__(self, parent=None):
* def init_objects(self):
* def init_section(self):
* def eventFilter(self, QObject, QEvent):
* def keyPressEvent(self, QKeyEvent):
* def timerEvent(self, e):
* def moving_ship(self):
* def fire(self):
* def find_section(self, x, y):
* def moving_missile(self):
* def moving_section(self, old, new, missile):
* def draw_ship(self,e,qp):
* def draw_missiles(self,e,qp):
* def mouseMoveEvent(self, QMouseEvent):
* def paintEvent(self, QPaintEvent):

## Code

Example Python PyQt program :

    # coding: utf-8
    
    import sys
    from PyQt5 import QtWidgets
    from PyQt5 import QtCore
    from PyQt5 import QtGui
    import time
    import random
    import math
    
    class SectionCon():
        missile_cnt = 0
    
        def __init__(self):
            self.con = []  # 미사일의 객체보관
    
    
        def add(self, missile):
            self.missile_cnt += 1
            self.con.append(missile)
    
        def remove(self):
            self.missile_cnt -= 1
            pass
    
    class Missile():
        number_of_missile = 0
        def __init__(self, x, y, th, v):
            self.x = x
            self.y = y
            self.r = 3
            self.theta = th
            self.v = v # 속도
            self.t = time.time()
    
        def draw(self, qp, sec_num):
            color =[
                QtCore.Qt.red,
                QtCore.Qt.blue,
                QtCore.Qt.gray,
                QtCore.Qt.green,
                QtCore.Qt.yellow,
                QtCore.Qt.black,
                QtCore.Qt.cyan,
                QtCore.Qt.darkMagenta,
                QtCore.Qt.darkRed,
            ]
    
    
            # 원을 그리는 함수
            # pen = QtGui.QPen(QtCore.Qt.red + sec_num, 1, QtCore.Qt.SolidLine)
            pen = QtGui.QPen(color[sec_num], 1, QtCore.Qt.SolidLine)
            qp.setPen(pen)
            qp.drawEllipse(self.x, self.y, self.r, self.r)
    
    
    class Ship():
        def __init__(self):
            self.x = 100
            self.y = 100
            self.t_gun_x = 0
            self.t_gun_y = 0
            self.r = 30
            self.theta = 0
            self.v = 1 # 속도
    
        def move_left(self):
            self.theta -= 0.1
    
        def move_right(self):
            self.theta += 0.1
    
    
        def move_up(self):
            self.v += 0.1
    
        def move_down(self):
            self.v -= 0.1
    
    
        def draw(self, qp):
            # 원을 그리는 함수
            pen = QtGui.QPen(QtCore.Qt.black, 1, QtCore.Qt.SolidLine)
            qp.setPen(pen)
            qp.drawEllipse(self.x, self.y, self.r, self.r)
            # 총구를 그린다
            pen = QtGui.QPen(QtCore.Qt.black, 1, QtCore.Qt.SolidLine)
            qp.setPen(pen)
            self.t_gun_x = (self.x + 25 * math.cos(self.theta)) + (self.r / 2)
            self.t_gun_y = self.y + 25 * math.sin(self.theta) + (self.r / 2)
            qp.drawLine(self.x + (self.r/2), self.y + (self.r/2), self.t_gun_x, self.t_gun_y)
    
    class Form(QtWidgets.QWidget):
        def __init__(self, parent=None):
            QtWidgets.QWidget.__init__(self, parent)
            self.setGeometry(100, 100, 720, 480)
            self.setMouseTracking(True)
            self.installEventFilter(self)
    
            self.missile = []
            self.init_objects()
            self.rt = QtCore.QBasicTimer()
            self.rt.start(11, self)
            self.pressed_key = []
    
    
        def init_objects(self):
            self.ww = self.width()
            self.wh = self.height()
            self.init_section()  # section 객체설정
            self.ship = Ship()
            self.missile = []
    
    
        def init_section(self):
            self.sections = []
            for i in range(9):
                self.sections.append(SectionCon())
    
    
        def eventFilter(self, QObject, QEvent):
            self.pressed_key = list(set(self.pressed_key))
            if QEvent.type() == QEvent.KeyPress:
                self.pressed_key.append(QEvent.key())
    
                if self.pressed_key.count(QtCore.Qt.Key_Left) and \
                    self.pressed_key.count(QtCore.Qt.Key_Space):
                    self.fire()
    
                elif self.pressed_key.count(QtCore.Qt.Key_Right) and \
                    self.pressed_key.count(QtCore.Qt.Key_Space):
                    self.fire()
    
            elif QEvent.type() == QEvent.KeyRelease:
                self.pressed_key.remove(QEvent.key())
    
            return False
    
        def keyPressEvent(self, QKeyEvent):
            if QKeyEvent.key() == QtCore.Qt.Key_Escape:
                self.init_objects()
    
            if QKeyEvent.key() == QtCore.Qt.Key_Space:
                self.fire()
    
            if QKeyEvent.key() == QtCore.Qt.Key_Left:
                self.ship.move_left()
            elif QKeyEvent.key() == QtCore.Qt.Key_Right:
                self.ship.move_right()
    
            if QKeyEvent.key() == QtCore.Qt.Key_Up:
                self.ship.move_up()
            elif QKeyEvent.key() == QtCore.Qt.Key_Down:
                self.ship.move_down()
    
        def timerEvent(self, e):
            self.moving_missile()
            self.moving_ship()
            self.repaint()
    
        def moving_ship(self):
            x = self.ship.x
            y = self.ship.y
            theta = self.ship.theta
            v = self.ship.v
    
            x += v * math.cos(theta)
            y += v * math.sin(theta)
    
            self.ship.x = x % self.width()
            self.ship.y = y % self.height()
    
        def fire(self):
            x = self.ship.t_gun_x
            y = self.ship.t_gun_y
            th = self.ship.theta
            v = self.ship.v + 2
            cur_section = self.find_section(x, y)
            self.sections[cur_section].add(Missile(x, y, th, v))
            # self.missile.append(Missile(x, y, th, v))
    
        def find_section(self, x, y):
            n = int((x // (self.ww / 3)) + ((y // (self.wh / 3)) * 3))
            return n
    
    
        def moving_missile(self):
            for i in range(len(self.sections)):
                if not self.sections[i].con:
                    continue
                else:
                    for j in range(len(self.sections[i].con)):
    
                        x = self.sections[i].con[j].x
                        y = self.sections[i].con[j].y
    
                        v = self.sections[i].con[j].v
    
                        x += v * math.cos(self.sections[i].con[j].theta)
                        y += v * math.sin(self.sections[i].con[j].theta)
    
                        sec_x = self.sections[i].con[j].x = x % self.width()
                        sec_y = self.sections[i].con[j].y = y % self.height()
    
                        sec_num = self.find_section(sec_x, sec_y)
                        self.moving_section(i, sec_num, j)
    
        def moving_section(self, old, new, missile):
            self.sections[new].con.append(
                self.sections[old].con.pop(missile)
            )
            
        def draw_ship(self,e,qp):
            self.ship.draw(qp)
    
        def draw_missiles(self,e,qp):
            i = 0
            for s in self.sections:
                for m in s.con:
                    m.draw(qp, i)
                i += 1
            # for m in self.missile:
            #     m.draw(qp)
    
        def mouseMoveEvent(self, QMouseEvent):
            self.mouse_x = QMouseEvent.x()
            self.mouse_y = QMouseEvent.y()
    
    
    
    
    
    
    
    
    
    
    
    
    
        def paintEvent(self, QPaintEvent):
            qp = QtGui.QPainter()
            qp.begin(self)
            self.draw_ship(QPaintEvent, qp)
            self.draw_missiles(QPaintEvent, qp)
            qp.drawText(20, 20,"x: %f, y: %f, v: %f, th: %f" % \
                            (self.ship.x, self.ship.y, self.ship.v, ((self.ship.theta * 180) / math.pi) % 360))
    
            qp.end()
    
    
    
    
    
    if __name__ == '__main__':
        app = QtWidgets.QApplication(sys.argv)
        # app.processEvents(QtCore.QEventLoop.AllEvents)
        w = Form()
        w.show()
        sys.exit(app.exec())
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/

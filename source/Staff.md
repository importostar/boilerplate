---
title: Staff
date: 2020-05-07
---
Example Python program Staff.py
This program creates a PyQt GUI

## Modules

* from PyQt5.QtWidgets import *
* from PyQt5.QtGui import *
* from PyQt5.QtCore import *
* from random import random, randint
* import sys

## Classes

* class StaffMainWindow(QWidget):

## Methods

* def __init__(self):
* def initUI(self):
* def draw_note(self, qp, hl, pos_n, pos_x):
* def paintEvent(self, e):
* def keyPressEvent(self, e):

## Code

Example Python PyQt program :

    from PyQt5.QtWidgets import *
    from PyQt5.QtGui import *
    from PyQt5.QtCore import *
    
    from random import random, randint
    
    import sys
    
    
    class StaffMainWindow(QWidget):
        def __init__(self):
            super().__init__()
    
            self.request_width = 1000
            self.request_height = 500
    
            self.line_width = 1
            self.line_spacing = 10
            self.hl_spacing = 120
            self.stub_width = 20
            self.stf_top = 100
    
            self.h_mid = self.stf_top + self.line_spacing * 2
            self.l_mid = self.stf_top + self.line_spacing * 6 + self.hl_spacing
    
            self.s_name = ['do', 're', 'mi', 'fa', 'so', 'la', 'si']
            self.n_name = ['C', 'D', 'E', 'F', 'G', 'A', 'B']
    
            self.is_h = True
            self.is_show = False
            self.pos_x = 0
            self.level = 0
    
            self.cur_s_name = 'do'
            self.cur_n_name = 'C'
            self.cur_level_name = 1
    
            self.initUI()
    
        def initUI(self):
            self.setGeometry(0, 0, self.request_width, self.request_height)
            self.setWindowTitle('Staff')
            self.show()
    
        def draw_note(self, qp, hl, pos_n, pos_x):
            if hl == 'h':
                cur_mid = self.h_mid
            else:
                cur_mid = self.l_mid
    
            if pos_n > 0:
                for i in range(7):
                    if i <= pos_n:
                        qp.drawRect(pos_x, cur_mid - i*self.line_spacing, self.stub_width, self.line_width)
                    else:
                        break
            else:
                for i in range(7):
                    if -i >= pos_n:
                        qp.drawRect(pos_x, cur_mid + i * self.line_spacing, self.stub_width, self.line_width)
                    else:
                        break
            qp.drawEllipse(pos_x + int(self.stub_width*0.1), cur_mid - int(pos_n * self.line_spacing)
                           - int(self.line_spacing*0.5),
                           int(self.stub_width*0.8), int(self.line_spacing*0.9))
    
        def paintEvent(self, e):
            qp = QPainter(self)
            qp.setBrush(QColor(0,0, 0, 255))
            for i in range(5):
                qp.drawRect(0, self.stf_top + self.line_spacing * i, self.width(), self.line_width)
            for i in range(5):
                qp.drawRect(0, self.stf_top + self.line_spacing * (i+4) + self.hl_spacing, self.width(), self.line_width)
            if self.is_h:
                self.draw_note(qp, 'h', self.level / 2, self.pos_x)
            else:
                self.draw_note(qp, 'l', self.level / 2, self.pos_x)
    
            qp.setFont(QFont("", 60))
            qp.setPen(QColor(0, 0, 0, 255))
            if self.is_show:
                qp.drawText(420, 400, self.cur_s_name + " " + str(self.cur_level_name) + " " + self.cur_n_name)
    
        def keyPressEvent(self, e):
            if e.key() == Qt.Key_N:
                self.level = self.level + randint(-3, 3) if randint(0, 7) else randint(-10, 10)
                if self.level > 12:
                    self.level = 12
                if self.level < -12:
                    self.level = -12
                self.pos_x = int(random()*self.request_width)
                self.is_h = randint(0, 6) if self.is_h else not randint(0, 6)
                if self.is_h:
                    self.cur_s_name = self.s_name[(self.level + 6) % 7]
                    self.cur_n_name = self.n_name[(self.level + 6) % 7]
                    self.cur_level_name = (self.level + 6) % 7 + 1
                else:
                    self.cur_s_name = self.s_name[(self.level + 1) % 7]
                    self.cur_n_name = self.n_name[(self.level + 1) % 7]
                    self.cur_level_name = (self.level + 1) % 7 + 1
            if e.key() == Qt.Key_S:
                self.is_show = True
            if e.key() == Qt.Key_X:
                self.is_show = False
            self.update()
    
    
    
    
    if __name__ == '__main__':
        app = QApplication(sys.argv)
        ex = StaffMainWindow()
        sys.exit(app.exec_())

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/

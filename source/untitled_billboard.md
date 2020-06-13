---
title: untitled_billboard
date: 2020-05-07
---
Example Python program untitled_billboard.py
This program creates a PyQt GUI

## Modules

* import sys
* from PyQt5.QtWidgets import (QGridLayout, QPushButton, QTableWidget,
* from PyQt5 import QtCore
* import release, Suspension_box, Database

## Classes

* class billboard(QWidget):

## Methods

* def __init__(self):
* def initUI(self):
* def changeEvent(self, event):
* def scr_set(self):
* def table_set(self):
* def billboard_open_release(self):
* def billboard_inquire(self):

## Code

Example Python PyQt program :

    import sys
    from PyQt5.QtWidgets import (QGridLayout, QPushButton, QTableWidget,
                                 QScrollBar, QApplication, QWidget, QTableWidgetItem)
    from PyQt5 import QtCore
    import release, Suspension_box, Database
    
    
    class billboard(QWidget):
        def __init__(self):
            super().__init__()
            self.box = ''
            self.Col = ('序號', '發佈者', '內容', '開始時間', '結束時間', '送給的部門')
            self.initUI()
            self.billboard_inquire()
    
        def initUI(self):
            self.setGeometry(300, 300, 650, 400)
            self.setWindowTitle('公佈欄')
    
            self.scr = QScrollBar()
            self.scr.setOrientation(QtCore.Qt.Horizontal)
            self.tab = QTableWidget()
            self.btn_release = QPushButton('發佈')
    
            self.btn_release.clicked.connect(self.billboard_open_release)
            self.scr.valueChanged.connect(self.billboard_inquire)
    
            self.scr_set()
            self.table_set()
    
            self.grid = QGridLayout()
            self.grid.setSpacing(5)
    
            self.grid.addWidget(self.scr, 0, 0, 1, 2)
            self.grid.addWidget(self.tab, 1, 0, 1, 2)
            self.grid.addWidget(self.btn_release, 2, 0, 1, 2)
    
            self.setLayout(self.grid)
            self.show()
    
        def changeEvent(self, event):
            if event.type() == QtCore.QEvent.WindowStateChange:
                if self.windowState() & QtCore.Qt.WindowMinimized:
                    self.box = Suspension_box.Suspension_box()
            QWidget.changeEvent(self, event)
    
        def scr_set(self):
            self.scr.setMinimum(0)
            self.scr.setMaximum(100)
    
        def table_set(self):
            self.tab.setRowCount(10)
            self.tab.setColumnCount(6)
            self.tab.setItem(3, 1, QTableWidgetItem("TEXT"))
            for i in range(0, len(self.Col)):
                self.tab.setHorizontalHeaderItem(i, QTableWidgetItem(self.Col[i]))
            for _ in range(0, 10):
                self.tab.setVerticalHeaderItem(_, QTableWidgetItem(''))
    
        def billboard_open_release(self):
            self.release = release.release()
    
        def billboard_inquire(self):
            sql = ('SELECT * FROM content ')
            A = Database.MsSqlPrint(sql)[::-1]
            for _ in range(self.scr.value() * 10, self.scr.value() * 10 + 10):
                for i in range(6):
                    if _ <= len(A) - 1:
                        self.tab.setItem(_ % 10, i, QTableWidgetItem(str(A[_][i])))
                    else:
                        self.tab.setItem(_ % 10, i, QTableWidgetItem(''))
    
    
    if __name__ == '__main__':
        app = QApplication(sys.argv)
        ex = billboard()
        sys.exit(app.exec_())
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/

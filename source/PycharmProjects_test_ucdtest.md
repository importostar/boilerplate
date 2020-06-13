---
title: PycharmProjects_test_ucdtest
date: 2020-05-07
---
Example Python program PycharmProjects_test_ucdtest.py
This program creates a PyQt GUI

## Modules

* from PyQt5 import QtCore, QtGui, QtWidgets
* import random
* import sys

## Classes

* class MyWindow(QtWidgets.QMainWindow):

## Methods

* def setupUi(self, MainWindow):
* def retranslateUi(self, MainWindow):
* def operate(self):

## Code

Example Python PyQt program :

    # -*- coding: utf-8 -*-
    
    # Form implementation generated from reading ui file 'ucdtest.ui'
    #
    # Created by: PyQt5 UI code generator 5.6
    #
    # WARNING! All changes made in this file will be lost!
    
    from PyQt5 import QtCore, QtGui, QtWidgets
    import random
    class MyWindow(QtWidgets.QMainWindow):
        def setupUi(self, MainWindow):
            MainWindow.setObjectName("MainWindow")
            MainWindow.resize(800, 600)
            self.centralwidget = QtWidgets.QWidget(MainWindow)
            self.centralwidget.setObjectName("centralwidget")
            self.lcdNumber = QtWidgets.QLCDNumber(self.centralwidget)
            self.lcdNumber.setGeometry(QtCore.QRect(250, 90, 281, 131))
            self.lcdNumber.setObjectName("lcdNumber")
    
            self.menubar = QtWidgets.QMenuBar(MainWindow)
            self.menubar.setGeometry(QtCore.QRect(0, 0, 800, 21))
            self.menubar.setObjectName("menubar")
    
            self.statusbar = QtWidgets.QStatusBar(MainWindow)
            self.statusbar.setObjectName("statusbar")
    
            self.timer = QtCore.QTimer(self)  # 初始化一个定时器
            self.timer.timeout.connect(self.operate)  # 计时结束调用operate()方法
            self.timer.start(2000)  # 设置计时间隔并启动
            self.retranslateUi(MainWindow)
            QtCore.QMetaObject.connectSlotsByName(MainWindow)
    
    
    
        def retranslateUi(self, MainWindow):
            _translate = QtCore.QCoreApplication.translate
            MainWindow.setWindowTitle(_translate("MainWindow", "MainWindow"))
        def operate(self):
            num = random.randint(1, 20)
    
            self.lcdNumber.display(num)
    
    
    if __name__ == "__main__":
        import sys
    
        app = QtWidgets.QApplication(sys.argv)
        widget = QtWidgets.QWidget()
        myshow = MyWindow()
        myshow.setupUi(widget)
        widget.show()
        sys.exit(app.exec_())

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/

---
title: serwer_gui
date: 2020-05-07
---
Example Python program serwer_gui.py
This program creates a PyQt GUI

## Modules

* from PyQt5 import QtCore, QtGui, QtWidgets
* import sys

## Classes

* class Ui_MainWindow(object):

## Methods

* def setupUi(self, MainWindow):
* def retranslateUi(self, MainWindow):

## Code

Example Python PyQt program :

    # -*- coding: utf-8 -*-
    
    # Form implementation generated from reading ui file 'untitled.ui'
    #
    # Created by: PyQt5 UI code generator 5.9.2
    #
    # WARNING! All changes made in this file will be lost!
    
    from PyQt5 import QtCore, QtGui, QtWidgets
    
    class Ui_MainWindow(object):
        def setupUi(self, MainWindow):
            MainWindow.setObjectName("MainWindow")
            MainWindow.resize(314, 257)
            self.centralwidget = QtWidgets.QWidget(MainWindow)
            self.centralwidget.setObjectName("centralwidget")
            self.verticalLayout = QtWidgets.QVBoxLayout(self.centralwidget)
            self.verticalLayout.setObjectName("verticalLayout")
            self.pushButtonKlientClose = QtWidgets.QPushButton(self.centralwidget)
            self.pushButtonKlientClose.setObjectName("pushButtonKlientClose")
            self.verticalLayout.addWidget(self.pushButtonKlientClose)
            self.pushButtonCzasStart = QtWidgets.QPushButton(self.centralwidget)
            self.pushButtonCzasStart.setObjectName("pushButtonCzasStart")
            self.verticalLayout.addWidget(self.pushButtonCzasStart)
            self.spinBoxTime = QtWidgets.QSpinBox(self.centralwidget)
            self.spinBoxTime.setObjectName("spinBoxTime")
            self.verticalLayout.addWidget(self.spinBoxTime)
            MainWindow.setCentralWidget(self.centralwidget)
            self.menubar = QtWidgets.QMenuBar(MainWindow)
            self.menubar.setGeometry(QtCore.QRect(0, 0, 314, 25))
            self.menubar.setObjectName("menubar")
            MainWindow.setMenuBar(self.menubar)
            self.statusbar = QtWidgets.QStatusBar(MainWindow)
            self.statusbar.setObjectName("statusbar")
            MainWindow.setStatusBar(self.statusbar)
    
            self.retranslateUi(MainWindow)
            QtCore.QMetaObject.connectSlotsByName(MainWindow)
    
        def retranslateUi(self, MainWindow):
            _translate = QtCore.QCoreApplication.translate
            MainWindow.setWindowTitle(_translate("MainWindow", "MainWindow"))
            self.pushButtonKlientClose.setText(_translate("MainWindow", "pushButtonKlientClose"))
            self.pushButtonCzasStart.setText(_translate("MainWindow", "pushButtonCzasStart"))
    
    
    if __name__ == "__main__":
        import sys
        app = QtWidgets.QApplication(sys.argv)
        MainWindow = QtWidgets.QMainWindow()
        ui = Ui_MainWindow()
        ui.setupUi(MainWindow)
        MainWindow.show()
        sys.exit(app.exec_())
    
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/

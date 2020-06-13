---
title: MainWinTabOrder
date: 2020-05-07
---
Example Python program MainWinTabOrder.py

## Modules

* from PyQt5 import QtCore, QtGui, QtWidgets

## Classes

* class Ui_MainWindow(object):

## Methods

* def setupUi(self, MainWindow):
* def retranslateUi(self, MainWindow):

## Code

Example Python PyQt program :

    # -*- coding: utf-8 -*-
    
    # Form implementation generated from reading ui file 'MainWinTabOrder.ui'
    #
    # Created by: PyQt5 UI code generator 5.10.1
    #
    # WARNING! All changes made in this file will be lost!
    
    from PyQt5 import QtCore, QtGui, QtWidgets
    
    class Ui_MainWindow(object):
        def setupUi(self, MainWindow):
            MainWindow.setObjectName("MainWindow")
            MainWindow.resize(800, 600)
            self.centralwidget = QtWidgets.QWidget(MainWindow)
            self.centralwidget.setObjectName("centralwidget")
            self.lineEdit = QtWidgets.QLineEdit(self.centralwidget)
            self.lineEdit.setGeometry(QtCore.QRect(150, 20, 113, 25))
            self.lineEdit.setObjectName("lineEdit")
            self.lineEdit_2 = QtWidgets.QLineEdit(self.centralwidget)
            self.lineEdit_2.setGeometry(QtCore.QRect(170, 80, 113, 25))
            self.lineEdit_2.setObjectName("lineEdit_2")
            self.comboBox = QtWidgets.QComboBox(self.centralwidget)
            self.comboBox.setGeometry(QtCore.QRect(120, 140, 99, 24))
            self.comboBox.setObjectName("comboBox")
            self.lineEdit_3 = QtWidgets.QLineEdit(self.centralwidget)
            self.lineEdit_3.setGeometry(QtCore.QRect(80, 190, 113, 25))
            self.lineEdit_3.setObjectName("lineEdit_3")
            self.comboBox_2 = QtWidgets.QComboBox(self.centralwidget)
            self.comboBox_2.setGeometry(QtCore.QRect(210, 230, 99, 24))
            self.comboBox_2.setObjectName("comboBox_2")
            self.lineEdit_4 = QtWidgets.QLineEdit(self.centralwidget)
            self.lineEdit_4.setGeometry(QtCore.QRect(100, 320, 113, 25))
            self.lineEdit_4.setObjectName("lineEdit_4")
            MainWindow.setCentralWidget(self.centralwidget)
            self.menubar = QtWidgets.QMenuBar(MainWindow)
            self.menubar.setGeometry(QtCore.QRect(0, 0, 800, 30))
            self.menubar.setObjectName("menubar")
            MainWindow.setMenuBar(self.menubar)
            self.statusbar = QtWidgets.QStatusBar(MainWindow)
            self.statusbar.setObjectName("statusbar")
            MainWindow.setStatusBar(self.statusbar)
    
            self.retranslateUi(MainWindow)
            QtCore.QMetaObject.connectSlotsByName(MainWindow)
            MainWindow.setTabOrder(self.lineEdit_3, self.lineEdit)
            MainWindow.setTabOrder(self.lineEdit, self.lineEdit_2)
            MainWindow.setTabOrder(self.lineEdit_2, self.comboBox)
            MainWindow.setTabOrder(self.comboBox, self.comboBox_2)
            MainWindow.setTabOrder(self.comboBox_2, self.lineEdit_4)
    
        def retranslateUi(self, MainWindow):
            _translate = QtCore.QCoreApplication.translate
            MainWindow.setWindowTitle(_translate("MainWindow", "MainWindow"))
    
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/

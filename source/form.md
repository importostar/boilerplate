---
title: form
date: 2020-05-07
---
Example Python program form.py

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
    
    # Form implementation generated from reading ui file 'designer\form.ui'
    #
    # Created by: PyQt5 UI code generator 5.8.2
    #
    # WARNING! All changes made in this file will be lost!
    
    from PyQt5 import QtCore, QtGui, QtWidgets
    
    class Ui_MainWindow(object):
        def setupUi(self, MainWindow):
            MainWindow.setObjectName("MainWindow")
            MainWindow.resize(823, 493)
            self.centralwidget = QtWidgets.QWidget(MainWindow)
            self.centralwidget.setObjectName("centralwidget")
            self.verticalLayout_2 = QtWidgets.QVBoxLayout(self.centralwidget)
            self.verticalLayout_2.setObjectName("verticalLayout_2")
            self.verticalLayout = QtWidgets.QVBoxLayout()
            self.verticalLayout.setObjectName("verticalLayout")
            self.horizontalLayout = QtWidgets.QHBoxLayout()
            self.horizontalLayout.setObjectName("horizontalLayout")
            self.lineEdit = QtWidgets.QLineEdit(self.centralwidget)
            self.lineEdit.setObjectName("lineEdit")
            self.horizontalLayout.addWidget(self.lineEdit)
            self.pushButton = QtWidgets.QPushButton(self.centralwidget)
            self.pushButton.setObjectName("pushButton")
            self.horizontalLayout.addWidget(self.pushButton)
            self.verticalLayout.addLayout(self.horizontalLayout)
            self.tableWidget = QtWidgets.QTableWidget(self.centralwidget)
            self.tableWidget.setObjectName("tableVidget")
            self.verticalLayout.addWidget(self.tableWidget)
            self.verticalLayout_2.addLayout(self.verticalLayout)
            MainWindow.setCentralWidget(self.centralwidget)
            self.statusbar = QtWidgets.QStatusBar(MainWindow)
            self.statusbar.setObjectName("statusbar")
            MainWindow.setStatusBar(self.statusbar)
    
            self.retranslateUi(MainWindow)
            QtCore.QMetaObject.connectSlotsByName(MainWindow)
    
        def retranslateUi(self, MainWindow):
            _translate = QtCore.QCoreApplication.translate
            MainWindow.setWindowTitle(_translate("MainWindow", "MainWindow"))
            self.pushButton.setText(_translate("MainWindow", "PushButton"))
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/

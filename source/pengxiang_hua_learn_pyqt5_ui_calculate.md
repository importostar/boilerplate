---
title: pengxiang_hua_learn_pyqt5_ui_calculate
date: 2020-05-07
---
Example Python program pengxiang_hua_learn_pyqt5_ui_calculate.py

## Modules

* from PyQt5 import QtCore, QtGui, QtWidgets

## Classes

* class Ui_Calculate(object):

## Methods

* def setupUi(self, Calculate):
* def retranslateUi(self, Calculate):

## Code

Example Python PyQt program :

    # -*- coding: utf-8 -*-
    
    # Form implementation generated from reading ui file 'calculate.ui'
    #
    # Created by: PyQt5 UI code generator 5.13.0
    #
    # WARNING! All changes made in this file will be lost!
    
    
    from PyQt5 import QtCore, QtGui, QtWidgets
    
    
    class Ui_Calculate(object):
        def setupUi(self, Calculate):
            Calculate.setObjectName("Calculate")
            Calculate.resize(686, 444)
            self.centralwidget = QtWidgets.QWidget(Calculate)
            self.centralwidget.setObjectName("centralwidget")
            self.horizontalLayout = QtWidgets.QHBoxLayout(self.centralwidget)
            self.horizontalLayout.setObjectName("horizontalLayout")
            self.gridLayout = QtWidgets.QGridLayout()
            self.gridLayout.setObjectName("gridLayout")
            self.pushButton_20 = QtWidgets.QPushButton(self.centralwidget)
            self.pushButton_20.setObjectName("pushButton_20")
            self.gridLayout.addWidget(self.pushButton_20, 5, 3, 1, 1)
            self.pushButton_14 = QtWidgets.QPushButton(self.centralwidget)
            self.pushButton_14.setObjectName("pushButton_14")
            self.gridLayout.addWidget(self.pushButton_14, 3, 0, 1, 1)
            self.pushButton_12 = QtWidgets.QPushButton(self.centralwidget)
            self.pushButton_12.setObjectName("pushButton_12")
            self.gridLayout.addWidget(self.pushButton_12, 4, 0, 1, 1)
            self.pushButton_8 = QtWidgets.QPushButton(self.centralwidget)
            self.pushButton_8.setObjectName("pushButton_8")
            self.gridLayout.addWidget(self.pushButton_8, 2, 3, 1, 1)
            self.pushButton_9 = QtWidgets.QPushButton(self.centralwidget)
            self.pushButton_9.setObjectName("pushButton_9")
            self.gridLayout.addWidget(self.pushButton_9, 4, 1, 1, 1)
            self.pushButton_22 = QtWidgets.QPushButton(self.centralwidget)
            self.pushButton_22.setObjectName("pushButton_22")
            self.gridLayout.addWidget(self.pushButton_22, 5, 0, 1, 1)
            self.pushButton_2 = QtWidgets.QPushButton(self.centralwidget)
            self.pushButton_2.setObjectName("pushButton_2")
            self.gridLayout.addWidget(self.pushButton_2, 1, 1, 1, 1)
            self.lcdNumber = QtWidgets.QLCDNumber(self.centralwidget)
            self.lcdNumber.setObjectName("lcdNumber")
            self.gridLayout.addWidget(self.lcdNumber, 0, 0, 1, 4)
            self.pushButton_11 = QtWidgets.QPushButton(self.centralwidget)
            self.pushButton_11.setObjectName("pushButton_11")
            self.gridLayout.addWidget(self.pushButton_11, 4, 3, 1, 1)
            self.pushButton_23 = QtWidgets.QPushButton(self.centralwidget)
            self.pushButton_23.setObjectName("pushButton_23")
            self.gridLayout.addWidget(self.pushButton_23, 5, 1, 1, 1)
            self.pushButton_7 = QtWidgets.QPushButton(self.centralwidget)
            self.pushButton_7.setObjectName("pushButton_7")
            self.gridLayout.addWidget(self.pushButton_7, 2, 2, 1, 1)
            self.pushButton_6 = QtWidgets.QPushButton(self.centralwidget)
            self.pushButton_6.setObjectName("pushButton_6")
            self.gridLayout.addWidget(self.pushButton_6, 2, 1, 1, 1)
            self.pushButton_24 = QtWidgets.QPushButton(self.centralwidget)
            self.pushButton_24.setObjectName("pushButton_24")
            self.gridLayout.addWidget(self.pushButton_24, 5, 2, 1, 1)
            self.pushButton_13 = QtWidgets.QPushButton(self.centralwidget)
            self.pushButton_13.setObjectName("pushButton_13")
            self.gridLayout.addWidget(self.pushButton_13, 3, 3, 1, 1)
            self.pushButton_4 = QtWidgets.QPushButton(self.centralwidget)
            self.pushButton_4.setObjectName("pushButton_4")
            self.gridLayout.addWidget(self.pushButton_4, 1, 3, 1, 1)
            self.pushButton_15 = QtWidgets.QPushButton(self.centralwidget)
            self.pushButton_15.setObjectName("pushButton_15")
            self.gridLayout.addWidget(self.pushButton_15, 3, 1, 1, 1)
            self.pushButton = QtWidgets.QPushButton(self.centralwidget)
            self.pushButton.setObjectName("pushButton")
            self.gridLayout.addWidget(self.pushButton, 1, 0, 1, 1)
            self.pushButton_10 = QtWidgets.QPushButton(self.centralwidget)
            self.pushButton_10.setObjectName("pushButton_10")
            self.gridLayout.addWidget(self.pushButton_10, 4, 2, 1, 1)
            self.pushButton_16 = QtWidgets.QPushButton(self.centralwidget)
            self.pushButton_16.setObjectName("pushButton_16")
            self.gridLayout.addWidget(self.pushButton_16, 3, 2, 1, 1)
            self.pushButton_5 = QtWidgets.QPushButton(self.centralwidget)
            self.pushButton_5.setObjectName("pushButton_5")
            self.gridLayout.addWidget(self.pushButton_5, 2, 0, 1, 1)
            self.horizontalLayout.addLayout(self.gridLayout)
            Calculate.setCentralWidget(self.centralwidget)
            self.menubar = QtWidgets.QMenuBar(Calculate)
            self.menubar.setGeometry(QtCore.QRect(0, 0, 686, 26))
            self.menubar.setObjectName("menubar")
            Calculate.setMenuBar(self.menubar)
            self.statusbar = QtWidgets.QStatusBar(Calculate)
            self.statusbar.setObjectName("statusbar")
            Calculate.setStatusBar(self.statusbar)
    
            self.retranslateUi(Calculate)
            self.pushButton.clicked.connect(Calculate.calculate)
            self.pushButton_4.clicked.connect(Calculate.close)
            self.pushButton_22.clicked.connect(Calculate.record)
            self.pushButton_12.clicked.connect(Calculate.record)
            self.pushButton_14.clicked.connect(Calculate.record)
            self.pushButton_5.clicked.connect(Calculate.record)
            self.pushButton_2.clicked.connect(Calculate.record)
            self.pushButton_6.clicked.connect(Calculate.record)
            self.pushButton_15.clicked.connect(Calculate.record)
            self.pushButton_9.clicked.connect(Calculate.record)
            self.pushButton_23.clicked.connect(Calculate.record)
            self.pushButton_7.clicked.connect(Calculate.record)
            self.pushButton_16.clicked.connect(Calculate.record)
            self.pushButton_10.clicked.connect(Calculate.record)
            self.pushButton_24.clicked.connect(Calculate.calculate)
            self.pushButton_8.clicked.connect(Calculate.record)
            self.pushButton_13.clicked.connect(Calculate.record)
            self.pushButton_11.clicked.connect(Calculate.record)
            self.pushButton_20.clicked.connect(Calculate.record)
            QtCore.QMetaObject.connectSlotsByName(Calculate)
    
        def retranslateUi(self, Calculate):
            _translate = QtCore.QCoreApplication.translate
            Calculate.setWindowTitle(_translate("Calculate", "Calculate"))
            self.pushButton_20.setText(_translate("Calculate", "+"))
            self.pushButton_14.setText(_translate("Calculate", "4"))
            self.pushButton_12.setText(_translate("Calculate", "1"))
            self.pushButton_8.setText(_translate("Calculate", "/"))
            self.pushButton_9.setText(_translate("Calculate", "2"))
            self.pushButton_22.setText(_translate("Calculate", "0"))
            self.pushButton_2.setText(_translate("Calculate", "Back"))
            self.pushButton_11.setText(_translate("Calculate", "-"))
            self.pushButton_23.setText(_translate("Calculate", "."))
            self.pushButton_7.setText(_translate("Calculate", "9"))
            self.pushButton_6.setText(_translate("Calculate", "8"))
            self.pushButton_24.setText(_translate("Calculate", "="))
            self.pushButton_13.setText(_translate("Calculate", "*"))
            self.pushButton_4.setText(_translate("Calculate", "Close"))
            self.pushButton_15.setText(_translate("Calculate", "5"))
            self.pushButton.setText(_translate("Calculate", "Cls"))
            self.pushButton_10.setText(_translate("Calculate", "3"))
            self.pushButton_16.setText(_translate("Calculate", "6"))
            self.pushButton_5.setText(_translate("Calculate", "7"))
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/

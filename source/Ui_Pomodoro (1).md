---
title: Ui_Pomodoro (1)
date: 2020-05-07
---
Example Python program Ui_Pomodoro (1).py

## Modules

* from PyQt5 import QtCore, QtGui, QtWidgets

## Classes

* class Ui_Dialog(object):

## Methods

* def setupUi(self, Dialog):
* def retranslateUi(self, Dialog):

## Code

Example Python PyQt program :

    # -*- coding: utf-8 -*-
    
    # Form implementation generated from reading ui file 'd:\ben-code\python\pyqt5\project-promodoro\Pomodoro.ui'
    #
    # Created by: PyQt5 UI code generator 5.13.0
    #
    # WARNING! All changes made in this file will be lost!
    
    
    from PyQt5 import QtCore, QtGui, QtWidgets
    
    
    class Ui_Dialog(object):
        def setupUi(self, Dialog):
            Dialog.setObjectName("Dialog")
            Dialog.resize(382, 300)
            font = QtGui.QFont()
            font.setBold(False)
            font.setWeight(50)
            Dialog.setFont(font)
            self.labelMin = QtWidgets.QLabel(Dialog)
            self.labelMin.setGeometry(QtCore.QRect(20, 200, 31, 21))
            font = QtGui.QFont()
            font.setPointSize(10)
            font.setBold(False)
            font.setWeight(50)
            self.labelMin.setFont(font)
            self.labelMin.setAutoFillBackground(True)
            self.labelMin.setObjectName("labelMin")
            self.lcdNumber = QtWidgets.QLCDNumber(Dialog)
            self.lcdNumber.setGeometry(QtCore.QRect(10, 100, 91, 41))
            font = QtGui.QFont()
            font.setPointSize(9)
            font.setBold(False)
            font.setWeight(50)
            font.setStrikeOut(False)
            font.setKerning(False)
            self.lcdNumber.setFont(font)
            self.lcdNumber.setMode(QtWidgets.QLCDNumber.Dec)
            self.lcdNumber.setObjectName("lcdNumber")
            self.pushButtonStart = QtWidgets.QPushButton(Dialog)
            self.pushButtonStart.setGeometry(QtCore.QRect(90, 260, 93, 28))
            font = QtGui.QFont()
            font.setPointSize(12)
            font.setBold(False)
            font.setWeight(50)
            self.pushButtonStart.setFont(font)
            self.pushButtonStart.setObjectName("pushButtonStart")
            self.pushButtonStop = QtWidgets.QPushButton(Dialog)
            self.pushButtonStop.setGeometry(QtCore.QRect(190, 260, 93, 28))
            font = QtGui.QFont()
            font.setPointSize(12)
            font.setBold(False)
            font.setWeight(50)
            self.pushButtonStop.setFont(font)
            self.pushButtonStop.setObjectName("pushButtonStop")
            self.spinBoxMin = QtWidgets.QSpinBox(Dialog)
            self.spinBoxMin.setGeometry(QtCore.QRect(60, 200, 42, 22))
            self.spinBoxMin.setObjectName("spinBoxMin")
            self.labelSec = QtWidgets.QLabel(Dialog)
            self.labelSec.setGeometry(QtCore.QRect(20, 230, 31, 21))
            font = QtGui.QFont()
            font.setPointSize(10)
            font.setBold(False)
            font.setWeight(50)
            self.labelSec.setFont(font)
            self.labelSec.setAutoFillBackground(True)
            self.labelSec.setObjectName("labelSec")
            self.spinBoxSec = QtWidgets.QSpinBox(Dialog)
            self.spinBoxSec.setGeometry(QtCore.QRect(60, 230, 42, 22))
            self.spinBoxSec.setObjectName("spinBoxSec")
    
            self.retranslateUi(Dialog)
            QtCore.QMetaObject.connectSlotsByName(Dialog)
    
        def retranslateUi(self, Dialog):
            _translate = QtCore.QCoreApplication.translate
            Dialog.setWindowTitle(_translate("Dialog", "Dialog"))
            self.labelMin.setText(_translate("Dialog", "Mins"))
            self.pushButtonStart.setText(_translate("Dialog", "Start"))
            self.pushButtonStop.setText(_translate("Dialog", "Stop"))
            self.labelSec.setText(_translate("Dialog", "Sec"))
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/

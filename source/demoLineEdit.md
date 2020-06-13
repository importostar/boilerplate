---
title: demoLineEdit
date: 2020-05-07
---
Example Python program demoLineEdit.py

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
    
    # Form implementation generated from reading ui file 'demoLineEdit.ui'
    #
    # Created by: PyQt5 UI code generator 5.13.2
    #
    # WARNING! All changes made in this file will be lost!
    
    
    from PyQt5 import QtCore, QtGui, QtWidgets
    
    
    class Ui_Dialog(object):
        def setupUi(self, Dialog):
            Dialog.setObjectName("Dialog")
            Dialog.resize(425, 230)
            self.labelResponse = QtWidgets.QLabel(Dialog)
            self.labelResponse.setEnabled(True)
            self.labelResponse.setGeometry(QtCore.QRect(20, 50, 151, 31))
            font = QtGui.QFont()
            font.setFamily("MS Sans Serif")
            font.setPointSize(12)
            self.labelResponse.setFont(font)
            self.labelResponse.setObjectName("labelResponse")
            self.lineEditName = QtWidgets.QLineEdit(Dialog)
            self.lineEditName.setGeometry(QtCore.QRect(190, 50, 181, 31))
            font = QtGui.QFont()
            font.setFamily("MS Sans Serif")
            font.setPointSize(12)
            self.lineEditName.setFont(font)
            self.lineEditName.setObjectName("lineEditName")
            self.label = QtWidgets.QLabel(Dialog)
            self.label.setGeometry(QtCore.QRect(16, 100, 101, 20))
            font = QtGui.QFont()
            font.setFamily("MS Sans Serif")
            font.setPointSize(12)
            self.label.setFont(font)
            self.label.setObjectName("label")
            self.buttonClickMe = QtWidgets.QPushButton(Dialog)
            self.buttonClickMe.setGeometry(QtCore.QRect(190, 150, 75, 23))
            font = QtGui.QFont()
            font.setFamily("MS Sans Serif")
            font.setPointSize(12)
            self.buttonClickMe.setFont(font)
            self.buttonClickMe.setObjectName("buttonClickMe")
    
            self.retranslateUi(Dialog)
            QtCore.QMetaObject.connectSlotsByName(Dialog)
    
        def retranslateUi(self, Dialog):
            _translate = QtCore.QCoreApplication.translate
            Dialog.setWindowTitle(_translate("Dialog", "Dialog"))
            self.labelResponse.setText(_translate("Dialog", "Enter your name:"))
            self.label.setText(_translate("Dialog", "TextLabel"))
            self.buttonClickMe.setText(_translate("Dialog", "Click"))
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/

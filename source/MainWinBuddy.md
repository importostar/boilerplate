---
title: MainWinBuddy
date: 2020-05-07
---
Example Python program MainWinBuddy.py

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
    
    # Form implementation generated from reading ui file 'MainWinBuddy.ui'
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
            self.formLayoutWidget = QtWidgets.QWidget(self.centralwidget)
            self.formLayoutWidget.setGeometry(QtCore.QRect(90, 100, 431, 311))
            self.formLayoutWidget.setObjectName("formLayoutWidget")
            self.formLayout = QtWidgets.QFormLayout(self.formLayoutWidget)
            self.formLayout.setContentsMargins(0, 0, 0, 0)
            self.formLayout.setObjectName("formLayout")
            self.Label = QtWidgets.QLabel(self.formLayoutWidget)
            self.Label.setObjectName("Label")
            self.formLayout.setWidget(0, QtWidgets.QFormLayout.LabelRole, self.Label)
            self.LineEdit = QtWidgets.QLineEdit(self.formLayoutWidget)
            self.LineEdit.setObjectName("LineEdit")
            self.formLayout.setWidget(0, QtWidgets.QFormLayout.FieldRole, self.LineEdit)
            self.Label_2 = QtWidgets.QLabel(self.formLayoutWidget)
            self.Label_2.setObjectName("Label_2")
            self.formLayout.setWidget(1, QtWidgets.QFormLayout.LabelRole, self.Label_2)
            self.LineEdit_2 = QtWidgets.QLineEdit(self.formLayoutWidget)
            self.LineEdit_2.setObjectName("LineEdit_2")
            self.formLayout.setWidget(1, QtWidgets.QFormLayout.FieldRole, self.LineEdit_2)
            self.Label_3 = QtWidgets.QLabel(self.formLayoutWidget)
            self.Label_3.setObjectName("Label_3")
            self.formLayout.setWidget(2, QtWidgets.QFormLayout.LabelRole, self.Label_3)
            self.LineEdit_3 = QtWidgets.QLineEdit(self.formLayoutWidget)
            self.LineEdit_3.setObjectName("LineEdit_3")
            self.formLayout.setWidget(2, QtWidgets.QFormLayout.FieldRole, self.LineEdit_3)
            MainWindow.setCentralWidget(self.centralwidget)
            self.menubar = QtWidgets.QMenuBar(MainWindow)
            self.menubar.setGeometry(QtCore.QRect(0, 0, 800, 30))
            self.menubar.setObjectName("menubar")
            MainWindow.setMenuBar(self.menubar)
            self.statusbar = QtWidgets.QStatusBar(MainWindow)
            self.statusbar.setObjectName("statusbar")
            MainWindow.setStatusBar(self.statusbar)
            self.Label.setBuddy(self.LineEdit)
            self.Label_2.setBuddy(self.LineEdit_2)
            self.Label_3.setBuddy(self.LineEdit_3)
    
            self.retranslateUi(MainWindow)
            QtCore.QMetaObject.connectSlotsByName(MainWindow)
    
        def retranslateUi(self, MainWindow):
            _translate = QtCore.QCoreApplication.translate
            MainWindow.setWindowTitle(_translate("MainWindow", "MainWindow"))
            self.Label.setText(_translate("MainWindow", "暗搓搓(&A)"))
            self.Label_2.setText(_translate("MainWindow", "十点多(&B)"))
            self.Label_3.setText(_translate("MainWindow", "嗯嗯（&C）"))
    
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/

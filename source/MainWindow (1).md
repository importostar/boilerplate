---
title: MainWindow (1)
date: 2020-05-07
---
Example Python program MainWindow (1).py

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
    
    # Form implementation generated from reading ui file '.\MainWindow.ui'
    #
    # Created by: PyQt5 UI code generator 5.14.1
    #
    # WARNING! All changes made in this file will be lost!
    
    
    from PyQt5 import QtCore, QtGui, QtWidgets
    
    
    class Ui_MainWindow(object):
        def setupUi(self, MainWindow):
            MainWindow.setObjectName("MainWindow")
            MainWindow.resize(294, 222)
            self.centralwidget = QtWidgets.QWidget(MainWindow)
            self.centralwidget.setObjectName("centralwidget")
            self.gridLayout = QtWidgets.QGridLayout(self.centralwidget)
            self.gridLayout.setObjectName("gridLayout")
            self.formLayout = QtWidgets.QFormLayout()
            self.formLayout.setObjectName("formLayout")
            self.originalNumberLabel = QtWidgets.QLabel(self.centralwidget)
            self.originalNumberLabel.setObjectName("originalNumberLabel")
            self.formLayout.setWidget(0, QtWidgets.QFormLayout.LabelRole, self.originalNumberLabel)
            self.originalNumberLineEdit = QtWidgets.QLineEdit(self.centralwidget)
            self.originalNumberLineEdit.setObjectName("originalNumberLineEdit")
            self.formLayout.setWidget(0, QtWidgets.QFormLayout.FieldRole, self.originalNumberLineEdit)
            self.originalBaseLabel = QtWidgets.QLabel(self.centralwidget)
            self.originalBaseLabel.setObjectName("originalBaseLabel")
            self.formLayout.setWidget(1, QtWidgets.QFormLayout.LabelRole, self.originalBaseLabel)
            self.originalBaseLineEdit = QtWidgets.QLineEdit(self.centralwidget)
            self.originalBaseLineEdit.setObjectName("originalBaseLineEdit")
            self.formLayout.setWidget(1, QtWidgets.QFormLayout.FieldRole, self.originalBaseLineEdit)
            self.resultBaseLabel = QtWidgets.QLabel(self.centralwidget)
            self.resultBaseLabel.setObjectName("resultBaseLabel")
            self.formLayout.setWidget(2, QtWidgets.QFormLayout.LabelRole, self.resultBaseLabel)
            self.resultBaseLineEdit = QtWidgets.QLineEdit(self.centralwidget)
            self.resultBaseLineEdit.setObjectName("resultBaseLineEdit")
            self.formLayout.setWidget(2, QtWidgets.QFormLayout.FieldRole, self.resultBaseLineEdit)
            self.resultNumberLabel = QtWidgets.QLabel(self.centralwidget)
            self.resultNumberLabel.setObjectName("resultNumberLabel")
            self.formLayout.setWidget(3, QtWidgets.QFormLayout.LabelRole, self.resultNumberLabel)
            self.resultNumberLineEdit = QtWidgets.QLineEdit(self.centralwidget)
            self.resultNumberLineEdit.setObjectName("resultNumberLineEdit")
            self.formLayout.setWidget(3, QtWidgets.QFormLayout.FieldRole, self.resultNumberLineEdit)
            self.usingTableLabel = QtWidgets.QLabel(self.centralwidget)
            self.usingTableLabel.setObjectName("usingTableLabel")
            self.formLayout.setWidget(4, QtWidgets.QFormLayout.LabelRole, self.usingTableLabel)
            self.usingTableCheckBox = QtWidgets.QCheckBox(self.centralwidget)
            self.usingTableCheckBox.setObjectName("usingTableCheckBox")
            self.formLayout.setWidget(4, QtWidgets.QFormLayout.FieldRole, self.usingTableCheckBox)
            self.tableLabel = QtWidgets.QLabel(self.centralwidget)
            self.tableLabel.setEnabled(False)
            self.tableLabel.setObjectName("tableLabel")
            self.formLayout.setWidget(5, QtWidgets.QFormLayout.LabelRole, self.tableLabel)
            self.tableLineEdit = QtWidgets.QLineEdit(self.centralwidget)
            self.tableLineEdit.setEnabled(False)
            self.tableLineEdit.setObjectName("tableLineEdit")
            self.formLayout.setWidget(5, QtWidgets.QFormLayout.FieldRole, self.tableLineEdit)
            self.gridLayout.addLayout(self.formLayout, 0, 0, 1, 1)
            MainWindow.setCentralWidget(self.centralwidget)
            self.menubar = QtWidgets.QMenuBar(MainWindow)
            self.menubar.setGeometry(QtCore.QRect(0, 0, 294, 26))
            self.menubar.setObjectName("menubar")
            MainWindow.setMenuBar(self.menubar)
            self.statusbar = QtWidgets.QStatusBar(MainWindow)
            self.statusbar.setObjectName("statusbar")
            MainWindow.setStatusBar(self.statusbar)
    
            self.retranslateUi(MainWindow)
            self.usingTableCheckBox.clicked['bool'].connect(self.tableLabel.setEnabled)
            self.originalBaseLineEdit.textChanged['QString'].connect(self.originalNumberLineEdit.clear)
            self.originalBaseLineEdit.textChanged['QString'].connect(self.resultNumberLineEdit.clear)
            self.resultBaseLineEdit.textChanged['QString'].connect(self.originalNumberLineEdit.clear)
            self.resultBaseLineEdit.textChanged['QString'].connect(self.resultNumberLineEdit.clear)
            self.usingTableCheckBox.clicked['bool'].connect(self.tableLineEdit.setEnabled)
            self.tableLineEdit.textChanged['QString'].connect(self.originalNumberLineEdit.clear)
            self.tableLineEdit.textChanged['QString'].connect(self.resultNumberLineEdit.clear)
            self.usingTableCheckBox.toggled['bool'].connect(self.originalNumberLineEdit.clear)
            self.usingTableCheckBox.toggled['bool'].connect(self.resultNumberLineEdit.clear)
            QtCore.QMetaObject.connectSlotsByName(MainWindow)
    
        def retranslateUi(self, MainWindow):
            _translate = QtCore.QCoreApplication.translate
            MainWindow.setWindowTitle(_translate("MainWindow", "Base Converter"))
            self.originalNumberLabel.setText(_translate("MainWindow", "Original Number"))
            self.originalBaseLabel.setText(_translate("MainWindow", "Original Base"))
            self.resultBaseLabel.setText(_translate("MainWindow", "Result Base"))
            self.resultNumberLabel.setText(_translate("MainWindow", "Result Number"))
            self.usingTableLabel.setText(_translate("MainWindow", "Using Table"))
            self.tableLabel.setText(_translate("MainWindow", "Table"))
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/

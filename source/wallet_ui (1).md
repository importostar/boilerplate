---
title: wallet_ui (1)
date: 2020-05-07
---
Example Python program wallet_ui (1).py

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
    
    # Form implementation generated from reading ui file 'wallet.ui'
    #
    # Created by: PyQt5 UI code generator 5.10.1
    #
    # WARNING! All changes made in this file will be lost!
    
    from PyQt5 import QtCore, QtGui, QtWidgets
    
    class Ui_MainWindow(object):
        def setupUi(self, MainWindow):
            MainWindow.setObjectName("MainWindow")
            MainWindow.resize(807, 239)
            sizePolicy = QtWidgets.QSizePolicy(QtWidgets.QSizePolicy.Fixed, QtWidgets.QSizePolicy.Fixed)
            sizePolicy.setHorizontalStretch(0)
            sizePolicy.setVerticalStretch(0)
            sizePolicy.setHeightForWidth(MainWindow.sizePolicy().hasHeightForWidth())
            MainWindow.setSizePolicy(sizePolicy)
            self.centralwidget = QtWidgets.QWidget(MainWindow)
            self.centralwidget.setObjectName("centralwidget")
            self.horizontalLayoutWidget = QtWidgets.QWidget(self.centralwidget)
            self.horizontalLayoutWidget.setGeometry(QtCore.QRect(10, 20, 611, 31))
            self.horizontalLayoutWidget.setObjectName("horizontalLayoutWidget")
            self.horizontalLayout = QtWidgets.QHBoxLayout(self.horizontalLayoutWidget)
            self.horizontalLayout.setContentsMargins(0, 0, 0, 0)
            self.horizontalLayout.setObjectName("horizontalLayout")
            self.label = QtWidgets.QLabel(self.horizontalLayoutWidget)
            self.label.setObjectName("label")
            self.horizontalLayout.addWidget(self.label)
            self.accountLineEdit = QtWidgets.QLineEdit(self.horizontalLayoutWidget)
            self.accountLineEdit.setEnabled(False)
            self.accountLineEdit.setObjectName("accountLineEdit")
            self.horizontalLayout.addWidget(self.accountLineEdit)
            self.horizontalLayoutWidget_2 = QtWidgets.QWidget(self.centralwidget)
            self.horizontalLayoutWidget_2.setGeometry(QtCore.QRect(630, 20, 160, 31))
            self.horizontalLayoutWidget_2.setObjectName("horizontalLayoutWidget_2")
            self.horizontalLayout_2 = QtWidgets.QHBoxLayout(self.horizontalLayoutWidget_2)
            self.horizontalLayout_2.setContentsMargins(0, 0, 0, 0)
            self.horizontalLayout_2.setObjectName("horizontalLayout_2")
            self.balanceLineEdit = QtWidgets.QLineEdit(self.horizontalLayoutWidget_2)
            self.balanceLineEdit.setEnabled(False)
            self.balanceLineEdit.setObjectName("balanceLineEdit")
            self.horizontalLayout_2.addWidget(self.balanceLineEdit)
            self.horizontalLayoutWidget_3 = QtWidgets.QWidget(self.centralwidget)
            self.horizontalLayoutWidget_3.setGeometry(QtCore.QRect(10, 100, 611, 31))
            self.horizontalLayoutWidget_3.setObjectName("horizontalLayoutWidget_3")
            self.horizontalLayout_3 = QtWidgets.QHBoxLayout(self.horizontalLayoutWidget_3)
            self.horizontalLayout_3.setContentsMargins(0, 0, 0, 0)
            self.horizontalLayout_3.setObjectName("horizontalLayout_3")
            self.label_2 = QtWidgets.QLabel(self.horizontalLayoutWidget_3)
            self.label_2.setObjectName("label_2")
            self.horizontalLayout_3.addWidget(self.label_2)
            self.sendToLineEdit = QtWidgets.QLineEdit(self.horizontalLayoutWidget_3)
            self.sendToLineEdit.setObjectName("sendToLineEdit")
            self.horizontalLayout_3.addWidget(self.sendToLineEdit)
            self.horizontalLayoutWidget_4 = QtWidgets.QWidget(self.centralwidget)
            self.horizontalLayoutWidget_4.setGeometry(QtCore.QRect(630, 100, 160, 31))
            self.horizontalLayoutWidget_4.setObjectName("horizontalLayoutWidget_4")
            self.horizontalLayout_4 = QtWidgets.QHBoxLayout(self.horizontalLayoutWidget_4)
            self.horizontalLayout_4.setContentsMargins(0, 0, 0, 0)
            self.horizontalLayout_4.setObjectName("horizontalLayout_4")
            self.amountSendLineEdit = QtWidgets.QLineEdit(self.horizontalLayoutWidget_4)
            self.amountSendLineEdit.setObjectName("amountSendLineEdit")
            self.horizontalLayout_4.addWidget(self.amountSendLineEdit)
            self.sendButton = QtWidgets.QPushButton(self.centralwidget)
            self.sendButton.setGeometry(QtCore.QRect(10, 150, 781, 25))
            self.sendButton.setObjectName("sendButton")
            MainWindow.setCentralWidget(self.centralwidget)
            self.menubar = QtWidgets.QMenuBar(MainWindow)
            self.menubar.setGeometry(QtCore.QRect(0, 0, 807, 22))
            self.menubar.setObjectName("menubar")
            self.menuNew = QtWidgets.QMenu(self.menubar)
            self.menuNew.setObjectName("menuNew")
            MainWindow.setMenuBar(self.menubar)
            self.statusbar = QtWidgets.QStatusBar(MainWindow)
            self.statusbar.setObjectName("statusbar")
            MainWindow.setStatusBar(self.statusbar)
            self.actionNew = QtWidgets.QAction(MainWindow)
            self.actionNew.setObjectName("actionNew")
            self.actionOpen = QtWidgets.QAction(MainWindow)
            self.actionOpen.setObjectName("actionOpen")
            self.actionExit = QtWidgets.QAction(MainWindow)
            self.actionExit.setObjectName("actionExit")
            self.menuNew.addAction(self.actionNew)
            self.menuNew.addAction(self.actionOpen)
            self.menuNew.addSeparator()
            self.menuNew.addAction(self.actionExit)
            self.menubar.addAction(self.menuNew.menuAction())
    
            self.retranslateUi(MainWindow)
            QtCore.QMetaObject.connectSlotsByName(MainWindow)
    
        def retranslateUi(self, MainWindow):
            _translate = QtCore.QCoreApplication.translate
            MainWindow.setWindowTitle(_translate("MainWindow", "Genom Lite Wallet"))
            self.label.setText(_translate("MainWindow", "Account:"))
            self.label_2.setText(_translate("MainWindow", "Send To:"))
            self.sendButton.setText(_translate("MainWindow", "Send"))
            self.menuNew.setTitle(_translate("MainWindow", "Wallet"))
            self.actionNew.setText(_translate("MainWindow", "New"))
            self.actionOpen.setText(_translate("MainWindow", "Open"))
            self.actionExit.setText(_translate("MainWindow", "Exit"))
    
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/

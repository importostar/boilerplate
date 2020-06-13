---
title: MainWinsizepolicy
date: 2020-05-07
---
Example Python program MainWinsizepolicy.py

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
    
    # Form implementation generated from reading ui file 'MainWinsizepolicy.ui'
    #
    # Created by: PyQt5 UI code generator 5.10.1
    #
    # WARNING! All changes made in this file will be lost!
    
    from PyQt5 import QtCore, QtGui, QtWidgets
    
    class Ui_MainWindow(object):
        def setupUi(self, MainWindow):
            MainWindow.setObjectName("MainWindow")
            MainWindow.resize(825, 600)
            self.centralwidget = QtWidgets.QWidget(MainWindow)
            self.centralwidget.setObjectName("centralwidget")
            self.widget = QtWidgets.QWidget(self.centralwidget)
            self.widget.setGeometry(QtCore.QRect(40, 30, 721, 481))
            self.widget.setObjectName("widget")
            self.horizontalLayout = QtWidgets.QHBoxLayout(self.widget)
            self.horizontalLayout.setContentsMargins(0, 0, 0, 0)
            self.horizontalLayout.setObjectName("horizontalLayout")
            self.treeView = QtWidgets.QTreeView(self.widget)
            sizePolicy = QtWidgets.QSizePolicy(QtWidgets.QSizePolicy.Expanding, QtWidgets.QSizePolicy.Expanding)
            sizePolicy.setHorizontalStretch(1)
            sizePolicy.setVerticalStretch(0)
            sizePolicy.setHeightForWidth(self.treeView.sizePolicy().hasHeightForWidth())
            self.treeView.setSizePolicy(sizePolicy)
            self.treeView.setObjectName("treeView")
            self.horizontalLayout.addWidget(self.treeView)
            self.frame = QtWidgets.QFrame(self.widget)
            sizePolicy = QtWidgets.QSizePolicy(QtWidgets.QSizePolicy.Expanding, QtWidgets.QSizePolicy.Preferred)
            sizePolicy.setHorizontalStretch(2)
            sizePolicy.setVerticalStretch(0)
            sizePolicy.setHeightForWidth(self.frame.sizePolicy().hasHeightForWidth())
            self.frame.setSizePolicy(sizePolicy)
            self.frame.setFrameShape(QtWidgets.QFrame.StyledPanel)
            self.frame.setFrameShadow(QtWidgets.QFrame.Raised)
            self.frame.setObjectName("frame")
            self.formLayoutWidget = QtWidgets.QWidget(self.frame)
            self.formLayoutWidget.setGeometry(QtCore.QRect(110, 80, 281, 291))
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
            self.ComboBox = QtWidgets.QComboBox(self.formLayoutWidget)
            self.ComboBox.setObjectName("ComboBox")
            self.formLayout.setWidget(2, QtWidgets.QFormLayout.FieldRole, self.ComboBox)
            self.horizontalLayout.addWidget(self.frame)
            MainWindow.setCentralWidget(self.centralwidget)
            self.menubar = QtWidgets.QMenuBar(MainWindow)
            self.menubar.setGeometry(QtCore.QRect(0, 0, 825, 30))
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
            self.Label.setText(_translate("MainWindow", "姓名："))
            self.Label_2.setText(_translate("MainWindow", "年龄："))
            self.Label_3.setText(_translate("MainWindow", "性别："))
    
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/

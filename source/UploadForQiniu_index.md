---
title: UploadForQiniu_index
date: 2020-05-07
---
Example Python program UploadForQiniu_index.py

## Modules

* from PyQt5 import QtCore, QtGui, QtWidgets

## Classes

* class Ui_IndexWindow(object):

## Methods

* def setupUi(self, IndexWindow):
* def retranslateUi(self, IndexWindow):

## Code

Example Python PyQt program :

    # -*- coding: utf-8 -*-
    
    # Form implementation generated from reading ui file 'index.ui'
    #
    # Created by: PyQt5 UI code generator 5.9
    #
    # WARNING! All changes made in this file will be lost!
    
    from PyQt5 import QtCore, QtGui, QtWidgets
    
    class Ui_IndexWindow(object):
        def setupUi(self, IndexWindow):
            IndexWindow.setObjectName("IndexWindow")
            IndexWindow.resize(820, 645)
            self.centralwidget = QtWidgets.QWidget(IndexWindow)
            self.centralwidget.setObjectName("centralwidget")
            self.label = QtWidgets.QLabel(self.centralwidget)
            self.label.setGeometry(QtCore.QRect(60, 40, 120, 40))
            self.label.setObjectName("label")
            self.openFileBtn = QtWidgets.QToolButton(self.centralwidget)
            self.openFileBtn.setGeometry(QtCore.QRect(720, 160, 40, 40))
            self.openFileBtn.setObjectName("openFileBtn")
            self.label_2 = QtWidgets.QLabel(self.centralwidget)
            self.label_2.setGeometry(QtCore.QRect(60, 160, 120, 40))
            self.label_2.setObjectName("label_2")
            self.label_3 = QtWidgets.QLabel(self.centralwidget)
            self.label_3.setGeometry(QtCore.QRect(60, 220, 120, 41))
            self.label_3.setObjectName("label_3")
            self.bucketSpinner = QtWidgets.QComboBox(self.centralwidget)
            self.bucketSpinner.setGeometry(QtCore.QRect(180, 40, 580, 40))
            self.bucketSpinner.setObjectName("bucketSpinner")
            self.msgTextEdit = QtWidgets.QPlainTextEdit(self.centralwidget)
            self.msgTextEdit.setGeometry(QtCore.QRect(60, 340, 700, 200))
            self.msgTextEdit.setReadOnly(True)
            self.msgTextEdit.setObjectName("msgTextEdit")
            self.putFileBtn = QtWidgets.QPushButton(self.centralwidget)
            self.putFileBtn.setGeometry(QtCore.QRect(640, 560, 120, 40))
            self.putFileBtn.setObjectName("putFileBtn")
            self.progressLabel = QtWidgets.QLabel(self.centralwidget)
            self.progressLabel.setGeometry(QtCore.QRect(60, 560, 400, 40))
            self.progressLabel.setObjectName("progressLabel")
            self.label_4 = QtWidgets.QLabel(self.centralwidget)
            self.label_4.setGeometry(QtCore.QRect(60, 100, 120, 40))
            self.label_4.setObjectName("label_4")
            self.dirRadio = QtWidgets.QRadioButton(self.centralwidget)
            self.dirRadio.setGeometry(QtCore.QRect(180, 100, 132, 40))
            self.dirRadio.setChecked(True)
            self.dirRadio.setObjectName("dirRadio")
            self.fileRadio = QtWidgets.QRadioButton(self.centralwidget)
            self.fileRadio.setGeometry(QtCore.QRect(360, 100, 132, 40))
            self.fileRadio.setObjectName("fileRadio")
            self.originPathEdit = QtWidgets.QLineEdit(self.centralwidget)
            self.originPathEdit.setGeometry(QtCore.QRect(180, 160, 540, 40))
            self.originPathEdit.setObjectName("originPathEdit")
            self.destPathEdit = QtWidgets.QLineEdit(self.centralwidget)
            self.destPathEdit.setGeometry(QtCore.QRect(180, 220, 580, 40))
            self.destPathEdit.setObjectName("destPathEdit")
            self.label_5 = QtWidgets.QLabel(self.centralwidget)
            self.label_5.setGeometry(QtCore.QRect(60, 280, 120, 40))
            self.label_5.setObjectName("label_5")
            self.urlEdit = QtWidgets.QLineEdit(self.centralwidget)
            self.urlEdit.setEnabled(False)
            self.urlEdit.setGeometry(QtCore.QRect(180, 280, 580, 40))
            self.urlEdit.setReadOnly(True)
            self.urlEdit.setObjectName("urlEdit")
            IndexWindow.setCentralWidget(self.centralwidget)
            self.statusbar = QtWidgets.QStatusBar(IndexWindow)
            self.statusbar.setObjectName("statusbar")
            IndexWindow.setStatusBar(self.statusbar)
    
            self.retranslateUi(IndexWindow)
            QtCore.QMetaObject.connectSlotsByName(IndexWindow)
    
        def retranslateUi(self, IndexWindow):
            _translate = QtCore.QCoreApplication.translate
            IndexWindow.setWindowTitle(_translate("IndexWindow", "MainWindow"))
            self.label.setText(_translate("IndexWindow", "上传环境"))
            self.openFileBtn.setText(_translate("IndexWindow", "..."))
            self.label_2.setText(_translate("IndexWindow", "输入源地址"))
            self.label_3.setText(_translate("IndexWindow", "输入目标地址"))
            self.putFileBtn.setText(_translate("IndexWindow", "上传"))
            self.progressLabel.setText(_translate("IndexWindow", "当前进度：0%"))
            self.label_4.setText(_translate("IndexWindow", "文件类型"))
            self.dirRadio.setText(_translate("IndexWindow", "文件夹"))
            self.fileRadio.setText(_translate("IndexWindow", "文件"))
            self.label_5.setText(_translate("IndexWindow", "访问Url"))
    
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/
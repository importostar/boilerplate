---
title: home
date: 2020-05-07
---
Example Python program home.py

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
    
    # Form implementation generated from reading ui file 'home.ui'
    #
    # Created by: PyQt5 UI code generator 5.5.1
    #
    # WARNING! All changes made in this file will be lost!
    
    from PyQt5 import QtCore, QtGui, QtWidgets
    
    class Ui_Dialog(object):
        def setupUi(self, Dialog):
            Dialog.setObjectName("Dialog")
            Dialog.resize(352, 111)
            self.downloadAudio = QtWidgets.QPushButton(Dialog)
            self.downloadAudio.setGeometry(QtCore.QRect(0, 50, 351, 27))
            self.downloadAudio.setObjectName("downloadAudio")
            self.downloadVideo = QtWidgets.QPushButton(Dialog)
            self.downloadVideo.setGeometry(QtCore.QRect(0, 80, 351, 27))
            self.downloadVideo.setObjectName("downloadVideo")
            self.linkInput = QtWidgets.QLineEdit(Dialog)
            self.linkInput.setGeometry(QtCore.QRect(0, 0, 351, 27))
            self.linkInput.setText("")
            self.linkInput.setObjectName("linkInput")
            self.linkOkLabel = QtWidgets.QLabel(Dialog)
            self.linkOkLabel.setGeometry(QtCore.QRect(0, 30, 691, 17))
            self.linkOkLabel.setText("")
            self.linkOkLabel.setObjectName("linkOkLabel")
    
            self.retranslateUi(Dialog)
            QtCore.QMetaObject.connectSlotsByName(Dialog)
    
        def retranslateUi(self, Dialog):
            _translate = QtCore.QCoreApplication.translate
            Dialog.setWindowTitle(_translate("Dialog", "Dialog"))
            self.downloadAudio.setText(_translate("Dialog", "Download audio"))
            self.downloadVideo.setText(_translate("Dialog", "Download video"))
            self.linkInput.setPlaceholderText(_translate("Dialog", "Enter URL here..."))

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/

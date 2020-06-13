---
title: file_choosing
date: 2020-05-07
---
Example Python program file_choosing.py
This program creates a PyQt GUI

## Modules

* from PyQt5 import QtCore, QtGui, QtWidgets
* import sys

## Classes

* class Ui_Dialog(object):

## Methods

* def setupUi(self, Dialog):
* def retranslateUi(self, Dialog):

## Code

Example Python PyQt program :

    # -*- coding: utf-8 -*-
    
    # Form implementation generated from reading ui file 'file_choosing.ui'
    #
    # Created by: PyQt5 UI code generator 5.14.2
    #
    # WARNING! All changes made in this file will be lost!
    
    
    from PyQt5 import QtCore, QtGui, QtWidgets
    
    
    class Ui_Dialog(object):
        def setupUi(self, Dialog):
            Dialog.setObjectName("Dialog")
            Dialog.resize(677, 341)
            self.pushButton = QtWidgets.QPushButton(Dialog)
            self.pushButton.setGeometry(QtCore.QRect(530, 210, 101, 21))
            self.pushButton.setObjectName("pushButton")
            self.lineEdit = QtWidgets.QLineEdit(Dialog)
            self.lineEdit.setGeometry(QtCore.QRect(90, 32, 441, 31))
            self.lineEdit.setObjectName("lineEdit")
            self.label = QtWidgets.QLabel(Dialog)
            self.label.setGeometry(QtCore.QRect(40, 40, 31, 16))
            self.label.setObjectName("label")
            self.toolButton = QtWidgets.QToolButton(Dialog)
            self.toolButton.setGeometry(QtCore.QRect(540, 30, 81, 31))
            self.toolButton.setObjectName("toolButton")
            self.textBrowser = QtWidgets.QTextBrowser(Dialog)
            self.textBrowser.setGeometry(QtCore.QRect(40, 110, 391, 192))
            self.textBrowser.setObjectName("textBrowser")
            self.label_2 = QtWidgets.QLabel(Dialog)
            self.label_2.setGeometry(QtCore.QRect(220, 80, 59, 15))
            self.label_2.setObjectName("label_2")
    
            self.retranslateUi(Dialog)
            QtCore.QMetaObject.connectSlotsByName(Dialog)
    
        def retranslateUi(self, Dialog):
            _translate = QtCore.QCoreApplication.translate
            Dialog.setWindowTitle(_translate("Dialog", "Main"))
            self.pushButton.setText(_translate("Dialog", "OK"))
            self.label.setText(_translate("Dialog", "File"))
            self.toolButton.setText(_translate("Dialog", "Choose File"))
            self.label_2.setText(_translate("Dialog", "results"))
    
    
    if __name__ == "__main__":
        import sys
        app = QtWidgets.QApplication(sys.argv)
        Dialog = QtWidgets.QDialog()
        ui = Ui_Dialog()
        ui.setupUi(Dialog)
        Dialog.show()
        sys.exit(app.exec_())
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/

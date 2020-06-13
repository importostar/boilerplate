---
title: connectSQL_loginDisplay
date: 2020-05-07
---
Example Python program connectSQL_loginDisplay.py

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
    
    # Form implementation generated from reading ui file 'loginDisplay.ui'
    #
    # Created by: PyQt5 UI code generator 5.9.2
    #
    # WARNING! All changes made in this file will be lost!
    
    from PyQt5 import QtCore, QtGui, QtWidgets
    
    class Ui_Dialog(object):
        def setupUi(self, Dialog):
            Dialog.setObjectName("Dialog")
            Dialog.resize(340, 261)
            Dialog.setMinimumSize(QtCore.QSize(340, 261))
            Dialog.setMaximumSize(QtCore.QSize(340, 261))
            self.gridLayoutWidget = QtWidgets.QWidget(Dialog)
            self.gridLayoutWidget.setGeometry(QtCore.QRect(10, 10, 321, 239))
            self.gridLayoutWidget.setObjectName("gridLayoutWidget")
            self.user_Login = QtWidgets.QGridLayout(self.gridLayoutWidget)
            self.user_Login.setContentsMargins(7, 7, 7, 7)
            self.user_Login.setObjectName("user_Login")
            self.user_label = QtWidgets.QLabel(self.gridLayoutWidget)
            font = QtGui.QFont()
            font.setFamily("微软雅黑")
            self.user_label.setFont(font)
            self.user_label.setObjectName("user_label")
            self.user_Login.addWidget(self.user_label, 1, 0, 1, 1, QtCore.Qt.AlignHCenter)
            self.passwd_label = QtWidgets.QLabel(self.gridLayoutWidget)
            font = QtGui.QFont()
            font.setFamily("微软雅黑")
            self.passwd_label.setFont(font)
            self.passwd_label.setObjectName("passwd_label")
            self.user_Login.addWidget(self.passwd_label, 2, 0, 1, 1, QtCore.Qt.AlignHCenter)
            self.showsth_textBrowser = QtWidgets.QTextBrowser(self.gridLayoutWidget)
            self.showsth_textBrowser.setObjectName("showsth_textBrowser")
            self.user_Login.addWidget(self.showsth_textBrowser, 0, 0, 1, 4)
            self.login_Button = QtWidgets.QPushButton(self.gridLayoutWidget)
            font = QtGui.QFont()
            font.setFamily("微软雅黑")
            self.login_Button.setFont(font)
            self.login_Button.setObjectName("login_Button")
            self.user_Login.addWidget(self.login_Button, 4, 0, 1, 4)
            self.passwd_lineEdit = QtWidgets.QLineEdit(self.gridLayoutWidget)
            self.passwd_lineEdit.setEchoMode(QtWidgets.QLineEdit.Password)
            self.passwd_lineEdit.setObjectName("passwd_lineEdit")
            self.user_Login.addWidget(self.passwd_lineEdit, 2, 1, 1, 3)
            self.user_lineEdit = QtWidgets.QLineEdit(self.gridLayoutWidget)
            self.user_lineEdit.setObjectName("user_lineEdit")
            self.user_Login.addWidget(self.user_lineEdit, 1, 1, 1, 3)
            self.regit_Button = QtWidgets.QPushButton(self.gridLayoutWidget)
            self.regit_Button.setObjectName("regit_Button")
            self.user_Login.addWidget(self.regit_Button, 5, 0, 1, 4)
    
            self.retranslateUi(Dialog)
            QtCore.QMetaObject.connectSlotsByName(Dialog)
    
        def retranslateUi(self, Dialog):
            _translate = QtCore.QCoreApplication.translate
            Dialog.setWindowTitle(_translate("Dialog", "登录窗口-戢浩源201731064317"))
            self.user_label.setText(_translate("Dialog", "用户名"))
            self.passwd_label.setText(_translate("Dialog", "密码"))
            self.showsth_textBrowser.setHtml(_translate("Dialog", "<!DOCTYPE HTML PUBLIC \"-//W3C//DTD HTML 4.0//EN\" \"http://www.w3.org/TR/REC-html40/strict.dtd\">\n"
    "<html><head><meta name=\"qrichtext\" content=\"1\" /><style type=\"text/css\">\n"
    "p, li { white-space: pre-wrap; }\n"
    "</style></head><body style=\" font-family:\'SimSun\'; font-size:9pt; font-weight:400; font-style:normal;\">\n"
    "<p align=\"center\" style=\" margin-top:0px; margin-bottom:0px; margin-left:0px; margin-right:0px; -qt-block-indent:0; text-indent:0px;\">欢迎使用本系统</p></body></html>"))
            self.login_Button.setText(_translate("Dialog", "登录"))
            self.passwd_lineEdit.setPlaceholderText(_translate("Dialog", "请输入密码"))
            self.user_lineEdit.setPlaceholderText(_translate("Dialog", "请输入用户名"))
            self.regit_Button.setText(_translate("Dialog", "注册"))
    
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/

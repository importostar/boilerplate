---
title: chat_summit_cl_chat
date: 2020-05-07
---
Example Python program chat_summit_cl_chat.py
This program creates a PyQt GUI

## Modules

* from PyQt5 import QtCore, QtGui, QtWidgets
* from PyQt5.QtWidgets import *
* import sys

## Classes

* class Ui_MainWindow(object):
* class Mychat(QMainWindow, Ui_MainWindow):

## Methods

* def setupUi(self, MainWindow):
* def retranslateUi(self, MainWindow):
* def __init__(self):

## Code

Example Python PyQt program :

    # -*- coding: utf-8 -*-
    
    # Form implementation generated from reading ui file 'cl_chat.ui'
    #
    # Created by: PyQt5 UI code generator 5.11.3
    #
    # WARNING! All changes made in this file will be lost!
    
    from PyQt5 import QtCore, QtGui, QtWidgets
    from PyQt5.QtWidgets import *
    import sys
    
    class Ui_MainWindow(object):
        def setupUi(self, MainWindow):
            MainWindow.setObjectName("MainWindow")
            MainWindow.resize(664, 483)
            MainWindow.setMinimumSize(QtCore.QSize(580, 450))
            MainWindow.setIconSize(QtCore.QSize(30, 30))
            MainWindow.setAnimated(True)
            MainWindow.setUnifiedTitleAndToolBarOnMac(False)
            self.centralwidget = QtWidgets.QWidget(MainWindow)
            self.centralwidget.setObjectName("centralwidget")
            self.gridLayout = QtWidgets.QGridLayout(self.centralwidget)
            self.gridLayout.setSizeConstraint(QtWidgets.QLayout.SetDefaultConstraint)
            self.gridLayout.setContentsMargins(0, 0, 0, 0)
            self.gridLayout.setSpacing(0)
            self.gridLayout.setObjectName("gridLayout")
            self.horizontalFrame = QtWidgets.QFrame(self.centralwidget)
            self.horizontalFrame.setObjectName("horizontalFrame")
            self.horizontalLayout_2 = QtWidgets.QHBoxLayout(self.horizontalFrame)
            self.horizontalLayout_2.setContentsMargins(0, 0, -1, 0)
            self.horizontalLayout_2.setSpacing(0)
            self.horizontalLayout_2.setObjectName("horizontalLayout_2")
            self.name = QtWidgets.QLabel(self.horizontalFrame)
            self.name.setMinimumSize(QtCore.QSize(50, 50))
            self.name.setMaximumSize(QtCore.QSize(50, 50))
            self.name.setObjectName("name")
            self.horizontalLayout_2.addWidget(self.name)
            self.status = QtWidgets.QLabel(self.horizontalFrame)
            self.status.setMinimumSize(QtCore.QSize(50, 50))
            self.status.setMaximumSize(QtCore.QSize(50, 50))
            self.status.setObjectName("status")
            self.horizontalLayout_2.addWidget(self.status)
            spacerItem = QtWidgets.QSpacerItem(40, 20, QtWidgets.QSizePolicy.Expanding, QtWidgets.QSizePolicy.Minimum)
            self.horizontalLayout_2.addItem(spacerItem)
            self.info = QtWidgets.QLabel(self.horizontalFrame)
            self.info.setMinimumSize(QtCore.QSize(50, 50))
            self.info.setMaximumSize(QtCore.QSize(50, 50))
            self.info.setObjectName("info")
            self.horizontalLayout_2.addWidget(self.info)
            self.gridLayout.addWidget(self.horizontalFrame, 0, 6, 1, 1)
            self.sendbar = QtWidgets.QFrame(self.centralwidget)
            self.sendbar.setObjectName("sendbar")
            self.horizontalLayout = QtWidgets.QHBoxLayout(self.sendbar)
            self.horizontalLayout.setObjectName("horizontalLayout")
            self.vioce = QtWidgets.QPushButton(self.sendbar)
            self.vioce.setObjectName("vioce")
            self.horizontalLayout.addWidget(self.vioce)
            self.video = QtWidgets.QPushButton(self.sendbar)
            self.video.setObjectName("video")
            self.horizontalLayout.addWidget(self.video)
            self.file = QtWidgets.QPushButton(self.sendbar)
            self.file.setObjectName("file")
            self.horizontalLayout.addWidget(self.file)
            spacerItem1 = QtWidgets.QSpacerItem(40, 20, QtWidgets.QSizePolicy.Expanding, QtWidgets.QSizePolicy.Minimum)
            self.horizontalLayout.addItem(spacerItem1)
            self.send = QtWidgets.QPushButton(self.sendbar)
            self.send.setObjectName("send")
            self.horizontalLayout.addWidget(self.send)
            self.gridLayout.addWidget(self.sendbar, 2, 6, 1, 1)
            self.showwindow = QtWidgets.QTextBrowser(self.centralwidget)
            self.showwindow.setObjectName("showwindow")
            self.gridLayout.addWidget(self.showwindow, 1, 6, 1, 1)
            self.messageedit = QtWidgets.QTextEdit(self.centralwidget)
            self.messageedit.setMaximumSize(QtCore.QSize(16777215, 111))
            self.messageedit.setAutoFillBackground(True)
            self.messageedit.setObjectName("messageedit")
            self.gridLayout.addWidget(self.messageedit, 3, 6, 1, 1)
            self.openGLWidget = QtWidgets.QOpenGLWidget(self.centralwidget)
            self.openGLWidget.setObjectName("openGLWidget")
            self.gridLayout.addWidget(self.openGLWidget, 3, 2, 1, 1)
            self.showlist = QtWidgets.QTextBrowser(self.centralwidget)
            self.showlist.setMinimumSize(QtCore.QSize(250, 0))
            self.showlist.setMaximumSize(QtCore.QSize(250, 16777215))
            self.showlist.setTabStopWidth(80)
            self.showlist.setObjectName("showlist")
            self.gridLayout.addWidget(self.showlist, 0, 1, 4, 1)
            self.toolbar = QtWidgets.QWidget(self.centralwidget)
            self.toolbar.setMinimumSize(QtCore.QSize(50, 50))
            self.toolbar.setMaximumSize(QtCore.QSize(50, 16777215))
            self.toolbar.setAutoFillBackground(False)
            self.toolbar.setStyleSheet("QWidget{\n"
    "ackground-color =yellow; boder=2px}")
            self.toolbar.setObjectName("toolbar")
            self.verticalLayout = QtWidgets.QVBoxLayout(self.toolbar)
            self.verticalLayout.setContentsMargins(0, 0, 0, 0)
            self.verticalLayout.setSpacing(0)
            self.verticalLayout.setObjectName("verticalLayout")
            self.photo = QtWidgets.QLabel(self.toolbar)
            self.photo.setMinimumSize(QtCore.QSize(50, 50))
            self.photo.setMaximumSize(QtCore.QSize(50, 16777215))
            self.photo.setBaseSize(QtCore.QSize(50, 50))
            self.photo.setObjectName("photo")
            self.verticalLayout.addWidget(self.photo)
            self.chat = QtWidgets.QLabel(self.toolbar)
            self.chat.setMinimumSize(QtCore.QSize(50, 50))
            self.chat.setMaximumSize(QtCore.QSize(50, 16777215))
            self.chat.setBaseSize(QtCore.QSize(50, 50))
            self.chat.setObjectName("chat")
            self.verticalLayout.addWidget(self.chat)
            self.friends = QtWidgets.QLabel(self.toolbar)
            self.friends.setMinimumSize(QtCore.QSize(50, 50))
            self.friends.setMaximumSize(QtCore.QSize(50, 16777215))
            self.friends.setBaseSize(QtCore.QSize(50, 50))
            self.friends.setObjectName("friends")
            self.verticalLayout.addWidget(self.friends)
            self.function = QtWidgets.QLabel(self.toolbar)
            self.function.setMinimumSize(QtCore.QSize(50, 50))
            self.function.setMaximumSize(QtCore.QSize(23, 50))
            self.function.setBaseSize(QtCore.QSize(50, 50))
            self.function.setObjectName("function")
            self.verticalLayout.addWidget(self.function)
            spacerItem2 = QtWidgets.QSpacerItem(20, 40, QtWidgets.QSizePolicy.Minimum, QtWidgets.QSizePolicy.Expanding)
            self.verticalLayout.addItem(spacerItem2)
            self.setting = QtWidgets.QPushButton(self.toolbar)
            self.setting.setMinimumSize(QtCore.QSize(50, 50))
            self.setting.setMaximumSize(QtCore.QSize(50, 50))
            self.setting.setIconSize(QtCore.QSize(0, 0))
            self.setting.setObjectName("setting")
            self.verticalLayout.addWidget(self.setting)
            self.gridLayout.addWidget(self.toolbar, 0, 0, 4, 1)
            MainWindow.setCentralWidget(self.centralwidget)
    
            self.retranslateUi(MainWindow)
            QtCore.QMetaObject.connectSlotsByName(MainWindow)
    
        def retranslateUi(self, MainWindow):
            _translate = QtCore.QCoreApplication.translate
            MainWindow.setWindowTitle(_translate("MainWindow", "MainWindow"))
            self.name.setText(_translate("MainWindow", "name"))
            self.status.setText(_translate("MainWindow", "status"))
            self.info.setText(_translate("MainWindow", "info"))
            self.vioce.setText(_translate("MainWindow", "vioce"))
            self.video.setText(_translate("MainWindow", "video"))
            self.file.setText(_translate("MainWindow", "file"))
            self.send.setText(_translate("MainWindow", "send"))
            self.photo.setText(_translate("MainWindow", ""))
            self.chat.setText(_translate("MainWindow", ""))
            self.friends.setText(_translate("MainWindow", ""))
            self.function.setText(_translate("MainWindow", ""))
            self.setting.setText(_translate("MainWindow", ""))
    
    class Mychat(QMainWindow, Ui_MainWindow):
    
        def __init__(self):
            super().__init__()
            self.setupUi(self)
            qss_file = open('view/qss/chatwindow_style.qss').read()
            self.setStyleSheet(qss_file)
    
    if __name__ == "__main__":
        app = QtWidgets.QApplication(sys.argv)
        window = Mychat()
        window.show()
        sys.exit(app.exec_())

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/

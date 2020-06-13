---
title: MlabDemo (1)
date: 2020-05-07
---
Example Python program MlabDemo (1).py

## Modules

* from PyQt5 import QtCore, QtGui, QtWidgets
* from PyQt5.QtCore import QCoreApplication

## Classes

* class MlabDemo(object):

## Methods

* def setupUi(self, MlabDemo):
* def deviceState1(self):
* def deviceState2(self):
* def deviceState3(self):
* def deviceStateAll(self):
* def retranslateUi(self, MlabDemo):

## Code

Example Python PyQt program :

    # -*- coding: utf-8 -*-
    
    # Form implementation generated from reading ui file 'MlabDemo.ui'
    #
    # Created: Sat Jul 23 20:18:46 2016
    #      by: PyQt5 UI code generator 5.2.1
    #
    # WARNING! All changes made in this file will be lost!
    
    from PyQt5 import QtCore, QtGui, QtWidgets
    from PyQt5.QtCore import QCoreApplication
    
    class MlabDemo(object):
        def setupUi(self, MlabDemo):
            MlabDemo.setObjectName("MlabDemo")
            MlabDemo.resize(338, 273)
            self.widget = QtWidgets.QWidget(MlabDemo)
            self.widget.setGeometry(QtCore.QRect(-10, -1, 411, 281))
            self.widget.setStyleSheet("background-color: rgb(255, 255, 127);")
            self.widget.setObjectName("widget")
            self.grbC = QtWidgets.QGroupBox(self.widget)
            self.grbC.setGeometry(QtCore.QRect(20, 10, 141, 151))
            self.grbC.setStyleSheet("background-color: rgb(0, 255, 255);")
            self.grbC.setObjectName("grbC")
            # tạo push button : device1 ------------------------------- 
            self.device1 = QtWidgets.QPushButton(self.grbC)
            self.device1.setGeometry(QtCore.QRect(20, 30, 99, 27))
            self.device1.setStyleSheet("background-color: rgb(255, 170, 127);")
            self.device1.setCheckable(True)
            self.device1.setObjectName("device1")
            self.device1.clicked.connect(self.deviceState1)  # gọi tới chươn trình deviceState1() khi push button : device1 nhấn                                                                                                                                                  
    
            # tạo push button : device2 ---------------------------------
            self.device2 = QtWidgets.QPushButton(self.grbC)
            self.device2.setGeometry(QtCore.QRect(20, 70, 99, 27))
            self.device2.setStyleSheet("background-color: rgb(255, 170, 255);")
            self.device2.setCheckable(True)
            self.device2.setObjectName("device2")
            self.device2.clicked.connect(self.deviceState2)  # gọi tới chươn trình deviceState2() khi push button : device2 nhấn
    
            # tạo push button : device3  --------------------------------
            self.device3 = QtWidgets.QPushButton(self.grbC)
            self.device3.setGeometry(QtCore.QRect(20, 110, 99, 27))
            self.device3.setStyleSheet("background-color: rgb(170, 170, 255);")
            self.device3.setCheckable(True)
            self.device3.setObjectName("device3")
            self.device3.clicked.connect(self.deviceState3)  # gọi tới chươn trình deviceState3() khi push button : device2 nhấn
            
            # tạo radio button : turnoff  -------------------------------
            self.turnoff = QtWidgets.QRadioButton(self.widget)
            self.turnoff.setGeometry(QtCore.QRect(30, 170, 117, 22))
            self.turnoff.setStyleSheet("background-color: rgb(0, 170, 0);")
            self.turnoff.setObjectName("turnoff")
            self.turnoff.clicked.connect(self.deviceStateAll) # gọi tới chương trình deviceStateAll() khi close button : turnoff nhấn 
    
            self.grbD = QtWidgets.QGroupBox(self.widget)
            self.grbD.setGeometry(QtCore.QRect(170, 10, 171, 191))
            self.grbD.setStyleSheet("background-color: rgb(170, 255, 0);")
            self.grbD.setObjectName("grbD")
    
            # tạo label : deviceS1  --------------------------------
            self.deviceS1 = QtWidgets.QLabel(self.grbD)
            self.deviceS1.setGeometry(QtCore.QRect(10, 30, 151, 31))
            self.deviceS1.setStyleSheet("background-color: rgb(255, 170, 127);")
            self.deviceS1.setText("")
            self.deviceS1.setObjectName("deviceS1")
            if self.device1.isChecked():    # kiểm tra trạng thái của push button : device1 khi khởi động chương trình
                self.deviceS1.setText("Device 1 : ON")
            else:
                self.deviceS1.setText("Device 1 : OFF")
    
            # tạo label : deviceS2  --------------------------------
            self.deviceS2 = QtWidgets.QLabel(self.grbD)
            self.deviceS2.setGeometry(QtCore.QRect(10, 90, 151, 31))
            self.deviceS2.setStyleSheet("background-color: rgb(255, 170, 255);")
            self.deviceS2.setText("")
            self.deviceS2.setObjectName("deviceS2")
            if self.device2.isChecked():    # kiểm tra trạng thái của push button : device2 khi khởi động chương trình
                self.deviceS2.setText("Device 2 : ON")
            else:
                self.deviceS2.setText("Device 2 : OFF")
    
            # tạo label : deviceS3  --------------------------------
            self.deviceS3 = QtWidgets.QLabel(self.grbD)
            self.deviceS3.setGeometry(QtCore.QRect(10, 149, 151, 31))
            self.deviceS3.setStyleSheet("background-color: rgb(170, 170, 255);")
            self.deviceS3.setText("")
            self.deviceS3.setObjectName("deviceS3")
            if self.device3.isChecked():    # kiểm tra trạng thái của push button : device3 khi khởi động chương trình
                self.deviceS3.setText("Device 3 : ON")
            else:
                self.deviceS3.setText("Device 3 : OFF")
    
            # tạo push button : close -----------------------------
            self.close = QtWidgets.QPushButton(self.widget)
            self.close.setGeometry(QtCore.QRect(270, 240, 71, 27))
            self.close.setStyleSheet("background-color: rgb(255, 0, 0);")
            self.close.setObjectName("close")
            self.close.clicked.connect(QCoreApplication.instance().quit) # khi close được nhấn, dừng chương trình. 
            
    
            self.textEdit = QtWidgets.QTextEdit(self.widget)
            self.textEdit.setGeometry(QtCore.QRect(50, 230, 201, 31))
            self.textEdit.setStyleSheet("background-color: rgb(255, 255, 255);")
            self.textEdit.setObjectName("textEdit")
            self.retranslateUi(MlabDemo)
            QtCore.QMetaObject.connectSlotsByName(MlabDemo)
    
        def deviceState1(self):
            # when push button device1 clicked : Device state 1 = ON 
            # when push button device1 unclicked : Device state 1 = OFF
            if self.device1.isChecked():
                self.deviceS1.setText("Device 1 : ON")
            else:
                self.deviceS1.setText("Device 1 : OFF")
    
        def deviceState2(self):
            # when push button device2 clicked : Device state 2 = ON 
            # when push button device2 unclicked : Device state 2 = OFF
            if self.device2.isChecked():
                self.deviceS2.setText("Device 2 : ON")
            else:
                self.deviceS2.setText("Device 2 : OFF")
    
        def deviceState3(self):
            # when push button device3 clicked : Device state 3 = ON 
            # when push button device3 unclicked : Device state 3 = OFF
            if self.device3.isChecked():
                self.deviceS3.setText("Device 3 : ON")
            else:
                self.deviceS3.setText("Device 3 : OFF")
    
    
        def deviceStateAll(self):
            # when radio button is selected : turn off all davices
            # when radio button is deselected : none active
            if self.turnoff.isChecked():
                self.deviceS1.setText("Device 1 : OFF")
                self.deviceS2.setText("Device 2 : OFF")
                self.deviceS3.setText("Device 3 : OFF")
       
    
        def retranslateUi(self, MlabDemo):
            _translate = QtCore.QCoreApplication.translate
            MlabDemo.setWindowTitle(_translate("MlabDemo", "Dialog"))
            self.widget.setToolTip(_translate("MlabDemo", "<html><head/><body><p><br/></p></body></html>"))
            self.grbC.setTitle(_translate("MlabDemo", "Control"))
            self.device1.setText(_translate("MlabDemo", "Device1"))
            self.device2.setText(_translate("MlabDemo", "Device2"))
            self.device3.setText(_translate("MlabDemo", "Device3"))
            self.turnoff.setText(_translate("MlabDemo", "TurnOffAll"))
            self.grbD.setToolTip(_translate("MlabDemo", "<html><head/><body><p><br/></p></body></html>"))
            self.grbD.setTitle(_translate("MlabDemo", "Device States "))
            self.close.setText(_translate("MlabDemo", "Close"))
            self.textEdit.setHtml(_translate("MlabDemo", "<!DOCTYPE HTML PUBLIC \"-//W3C//DTD HTML 4.0//EN\" \"http://www.w3.org/TR/REC-html40/strict.dtd\">\n"
    "<html><head><meta name=\"qrichtext\" content=\"1\" /><style type=\"text/css\">\n"
    "p, li { white-space: pre-wrap; }\n"
    "</style></head><body style=\" font-family:\'Ubuntu\'; font-size:11pt; font-weight:400; font-style:normal;\">\n"
    "<p style=\" margin-top:0px; margin-bottom:0px; margin-left:0px; margin-right:0px; -qt-block-indent:0; text-indent:0px;\"><span style=\" font-weight:600; font-style:italic; color:#aa00ff;\">Mlab xin chao cac ban !!!</span></p></body></html>"))
    
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/

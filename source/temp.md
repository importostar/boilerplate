---
title: temp
date: 2020-05-07
---
Example Python program temp.py
This program creates a PyQt GUI

## Modules

* from PyQt5 import QtCore, QtGui, QtWidgets
* import sys

## Classes

* class Ui_MainWindow(object):

## Methods

* def setupUi(self, MainWindow):

## Code

Example Python PyQt program :

    # -*- coding: utf-8 -*-
    
    # Form implementation generated from reading ui file 'test.ui'
    #
    # Created by: PyQt5 UI code generator 5.13.1
    #
    # WARNING! All changes made in this file will be lost!
    
    
    from PyQt5 import QtCore, QtGui, QtWidgets
    
    
    class Ui_MainWindow(object):
        def setupUi(self, MainWindow):
            MainWindow.setObjectName("MainWindow")
            MainWindow.resize(800, 600)
            self.centralwidget = QtWidgets.QWidget(MainWindow)
            self.centralwidget.setObjectName("centralwidget")
            arr = ['paracetamol','jher kahle','marja patient','see you soon','depression']
            arr2 = ['500mg','400mg','400mg','200mg','100mg']
            for i in range(0,5):
                self.label = QtWidgets.QLabel(self.centralwidget)
                self.label.setGeometry(QtCore.QRect(40*(i+1),100*(i+1),200,50))
    
                self.textBrowser_3 = QtWidgets.QTextBrowser(self.centralwidget)
                self.textBrowser_3.setGeometry(QtCore.QRect(40*(i+1), 110*(i+1), 401, 131))
                self.textBrowser_3.viewport().setProperty("cursor", QtGui.QCursor(QtCore.Qt.PointingHandCursor))
                self.textBrowser_3.setMouseTracking(True)
                self.textBrowser_3.setTabletTracking(True)
                self.textBrowser_3.setAutoFillBackground(True)
                self.textBrowser_3.setStyleSheet("selection-background-color: qradialgradient(spread:pad, cx:0.5, cy:0.5, radius:0.5, fx:0.5, fy:0.5, stop:0 rgba(255, 255, 255, 255), stop:0.1 rgba(255, 255, 255, 255), stop:0.2 rgba(255, 176, 176, 167), stop:0.3 rgba(255, 151, 151, 92), stop:0.4 rgba(255, 125, 125, 51), stop:0.5 rgba(255, 76, 76, 205), stop:0.52 rgba(255, 76, 76, 205), stop:0.6 rgba(255, 180, 180, 84), stop:1 rgba(255, 255, 255, 0));")
                self.textBrowser_3.setObjectName("textBrowser_"+str(i))
                MainWindow.setCentralWidget(self.centralwidget)
                _translate = QtCore.QCoreApplication.translate
            
                MainWindow.setWindowTitle(_translate("MainWindow", "MainWindow"))
                self.label.setText(arr[i]+" "+arr2[i])
                # self.label.setObjectName()
                self.textBrowser_3.setHtml(_translate("MainWindow", "<!DOCTYPE HTML PUBLIC \"-//W3C//DTD HTML 4.0//EN\" \"http://www.w3.org/TR/REC-html40/strict.dtd\">\n"
        "<html><head><meta name=\"qrichtext\" content=\"1\" /><style type=\"text/css\">\n"
        "p, li { white-space: pre-wrap; }\n"
        "</style></head>{% block body %}style=\" font-family:\'Ubuntu\'; font-size:11pt; font-weight:400; font-style:normal;\">\n"
        "<p style=\" margin-top:0px; margin-bottom:0px; margin-left:0px; margin-right:0px; -qt-block-indent:0; text-indent:0px;\"><span style=\" font-family:\'MS Shell Dlg 2\'; font-size:8.25pt;\"> </span></p>\n"
        "<p style=\"-qt-paragraph-type:empty; margin-top:0px; margin-bottom:0px; margin-left:0px; margin-right:0px; -qt-block-indent:0; text-indent:0px; font-family:\'MS Shell Dlg 2\'; font-size:8.25pt;\"><br /></p>\n"
        "<p style=\" margin-top:0px; margin-bottom:0px; margin-left:0px; margin-right:0px; -qt-block-indent:0; text-indent:0px;\"><span style=\" font-family:\'MS Shell Dlg 2\'; font-size:8pt;\">1 tablet morning, noon &amp; after bed for 1<br />week </span></p><button>Raghav</button>{% endblock %}</html>"))
                
            QtCore.QMetaObject.connectSlotsByName(MainWindow)
    
    if __name__ == "__main__":
        import sys
        app = QtWidgets.QApplication(sys.argv)
        MainWindow = QtWidgets.QMainWindow()
        ui = Ui_MainWindow()
        ui.setupUi(MainWindow)
        MainWindow.show()
        sys.exit(app.exec_())
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/

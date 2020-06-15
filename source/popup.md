---
title: popup
date: 2020-05-07
---
Example Python program popup.py
This program creates a PyQt GUI
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import sys
* from PyQt5 import QtCore, QtWidgets

## Classes

* class Ui_FirstWindow(object) :
* class Ui_SecondWindow(object) :
* class Controller :

## Methods

* def setupUi(self, FirstWindow) :
* def retranslateUi(self, MainWindow) :
* def LoadSecondWindow(self) :
* def setupUi(self, SecondWindow) :
* def retranslateUi(self, MainWindow) :
* def __init__(self) :
* def Show_FirstWindow(self) :
* def Show_SecondWindow(self) :
* def Print(self) :

## Code

Example Python PyQt program :

    #create a popup window using a pushbutton in PyQt5
    import sys
    
    from PyQt5 import QtCore, QtWidgets
    
    class Ui_FirstWindow(object) :
        def setupUi(self, FirstWindow) :
            FirstWindow.setObjectName("FirstWindow")
            FirstWindow.resize(400, 300)
            self.centralWidget = QtWidgets.QWidget(FirstWindow)
            self.centralWidget.setObjectName("centralWidget")
            self.pushButton = QtWidgets.QPushButton(self.centralWidget)
            self.pushButton.setGeometry(QtCore.QRect(110, 130, 191, 23))
            self.pushButton.setObjectName("pushButton")
            FirstWindow.setCentralWidget(self.centralWidget)
    
            self.retranslateUi(FirstWindow)
            QtCore.QMetaObject.connectSlotsByName(FirstWindow)
    
        def retranslateUi(self, MainWindow) :
            _translate = QtCore.QCoreApplication.translate
            MainWindow.setWindowTitle(_translate("FirstWindow", "FirstWindow"))
            self.pushButton.setText(_translate("FirstWindow", "LoadSecondWindow"))
    
        def LoadSecondWindow(self) :
            SecondWindow = QtWidgets.QMainWindow()
            ui = Ui_SecondWindow()
            ui.setupUi(SecondWindow)
            SecondWindow.show()
    
    
    class Ui_SecondWindow(object) :
    
        def setupUi(self, SecondWindow) :
            SecondWindow.setObjectName("SecondWindow")
            SecondWindow.resize(400, 300)
            self.centralWidget = QtWidgets.QWidget(SecondWindow)
            self.centralWidget.setObjectName("centralWidget")
            self.pushButton = QtWidgets.QPushButton(self.centralWidget)
            self.pushButton.setGeometry(QtCore.QRect(110, 130, 191, 23))
            self.pushButton.setObjectName("pushButton")
            SecondWindow.setCentralWidget(self.centralWidget)
    
            self.retranslateUi(SecondWindow)
            QtCore.QMetaObject.connectSlotsByName(SecondWindow)
    
        def retranslateUi(self, MainWindow) :
            _translate = QtCore.QCoreApplication.translate
            MainWindow.setWindowTitle(_translate("SecondWindow", "SecondWindow"))
            self.pushButton.setText(_translate("SecondWindow", "Congratz !"))
    
    
    class Controller :
    
        def __init__(self) :
            pass
    
        def Show_FirstWindow(self) :
            self.FirstWindow = QtWidgets.QMainWindow()
            self.ui = Ui_FirstWindow()
            self.ui.setupUi(self.FirstWindow)
            self.ui.pushButton.clicked.connect(self.Show_SecondWindow)
    
            self.FirstWindow.show()
    
        def Show_SecondWindow(self) :
            self.SecondWindow = QtWidgets.QMainWindow()
            self.ui = Ui_SecondWindow()
            self.ui.setupUi(self.SecondWindow)
            self.ui.pushButton.clicked.connect(self.Print)
    
            self.SecondWindow.show()
    
        def Print(self) :
            print('After 99 hours of trying out everything')
    
    
    if __name__ == '__main__' :
        app = QtWidgets.QApplication(sys.argv)
        Controller = Controller()
        Controller.Show_FirstWindow()
        sys.exit(app.exec_())

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/

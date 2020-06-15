---
title: binary2
date: 2020-05-07
---
Example Python program binary2.py
This program creates a PyQt GUI

## Modules

* from PyQt5 import QtCore, QtGui, QtWidgets
* import sys

## Classes

* class Ui_MainWindow(object):

## Methods

* def setupUi(self, MainWindow):
* def binaryfunction(self):
* def retranslateUi(self, MainWindow):

## Code

Example Python PyQt program :

    from PyQt5 import QtCore, QtGui, QtWidgets
    
    class Ui_MainWindow(object):
        def setupUi(self, MainWindow):
            MainWindow.setObjectName("MainWindow")
            MainWindow.resize(800, 600)
            self.centralwidget = QtWidgets.QWidget(MainWindow)
            self.centralwidget.setObjectName("centralwidget")
            self.pushButton = QtWidgets.QPushButton(self.centralwidget)
            self.pushButton.setGeometry(QtCore.QRect(370, 220, 75, 23))
            self.pushButton.setObjectName("pushButton")
            #باانتخاب کلید تبدیل تابع دلخواه اجرا میشود
            self.pushButton.clicked.connect(self.binaryfunction)
            self.label = QtWidgets.QLabel(self.centralwidget)
            self.label.setGeometry(QtCore.QRect(150, 130, 121, 51))
            self.label.setStyleSheet("font: 75 16pt \"MS Shell Dlg 2\";")
            self.label.setObjectName("label")
            self.label_2 = QtWidgets.QLabel(self.centralwidget)
            self.label_2.setGeometry(QtCore.QRect(160, 270, 91, 51))
            self.label_2.setStyleSheet("font: 75 16pt \"MS Shell Dlg 2\";")
            self.label_2.setObjectName("label_2")
            self.lineEdit = QtWidgets.QLineEdit(self.centralwidget)
            self.lineEdit.setGeometry(QtCore.QRect(300, 120, 221, 81))
            self.lineEdit.setObjectName("lineEdit")
            self.lineEdit_2 = QtWidgets.QLineEdit(self.centralwidget)
            self.lineEdit_2.setGeometry(QtCore.QRect(300, 270, 221, 81))
            self.lineEdit_2.setObjectName("lineEdit_2")
            MainWindow.setCentralWidget(self.centralwidget)
            self.menubar = QtWidgets.QMenuBar(MainWindow)
            self.menubar.setGeometry(QtCore.QRect(0, 0, 800, 21))
            self.menubar.setObjectName("menubar")
            MainWindow.setMenuBar(self.menubar)
            self.statusbar = QtWidgets.QStatusBar(MainWindow)
            self.statusbar.setObjectName("statusbar")
            MainWindow.setStatusBar(self.statusbar)
    
            self.retranslateUi(MainWindow)
            QtCore.QMetaObject.connectSlotsByName(MainWindow)
            #نوشتن تابع تبدیل کننده
        def binaryfunction(self):
            #متن نوشته شده را در text می ریزیم
            text=self.lineEdit.text()
            #به صورت زیر متن را به کد بانری تبدیل میکنیم
            self.lineEdit_2.setText(' '.join(format(ord(x), 'b') for x in text)) 
            
        def retranslateUi(self, MainWindow):
            _translate = QtCore.QCoreApplication.translate
            MainWindow.setWindowTitle(_translate("MainWindow", "MainWindow"))
            self.pushButton.setText(_translate("MainWindow", "تبدیل"))
            self.label.setText(_translate("MainWindow", "متن انگلیسی"))
            self.label_2.setText(_translate("MainWindow", "کد باینری"))
    
    
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

---
title: hashmeld
date: 2020-05-07
---
Example Python program hashmeld.py
This program creates a PyQt GUI
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* from PyQt5 import QtCore, QtGui, QtWidgets
* from PyQt5.QtGui import QIcon
* import hashlib
* import sys

## Classes

* class Ui_Dialog(object):

## Methods

* def get_hash_md5(filename):
* def setupUi(self, Dialog):
* def buttonClicked(self):
* def buttonClicked2(self):
* def buttonClicked3(self):
* def save_to_file(self):
* def retranslateUi(self, Dialog):

## Code

Example Python PyQt program :

    # -*- coding: utf-8 -*-
    
    # Form implementation generated from reading ui file 'untitled.ui'
    #
    # Created by: PyQt5 UI code generator 5.13.2
    #
    # WARNING! All changes made in this file will be lost!
    
    
    from PyQt5 import QtCore, QtGui, QtWidgets
    from PyQt5.QtGui import QIcon
    import hashlib
    def get_hash_md5(filename):
        with open(filename, 'rb') as f:
            m = hashlib.md5()
            while True:
                data = f.read(8192)
                if not data:
                    break
                m.update(data)
            return m.hexdigest()
    
    is_savefile=0
    class Ui_Dialog(object):
        def setupUi(self, Dialog):
            Dialog.setObjectName("Dialog")
            Dialog.resize(400, 140)
            self.pushButton = QtWidgets.QPushButton(Dialog)
            self.pushButton.setGeometry(QtCore.QRect(40, 110, 75, 23))
            self.pushButton.setObjectName("pushButton")
            self.lineEdit = QtWidgets.QLineEdit(Dialog)
            self.lineEdit.setGeometry(QtCore.QRect(70, 10, 281, 20))
            self.lineEdit.setObjectName("lineEdit")
            self.lineEdit_2 = QtWidgets.QLineEdit(Dialog)
            self.lineEdit_2.setGeometry(QtCore.QRect(70, 60, 281, 20))
            self.lineEdit_2.setObjectName("lineEdit_2")
            self.label = QtWidgets.QLabel(Dialog)
            self.label.setGeometry(QtCore.QRect(10, 10, 61, 21))
            self.label.setObjectName("label")
            self.label_2 = QtWidgets.QLabel(Dialog)
            self.label_2.setGeometry(QtCore.QRect(10, 60, 61, 21))
            self.label_2.setObjectName("label_2")
            self.label_3 = QtWidgets.QLabel(Dialog)
            self.label_3.setGeometry(QtCore.QRect(50, 30, 341, 31))
            self.label_3.setObjectName("label_3")
            self.label_4 = QtWidgets.QLabel(Dialog)
            self.label_4.setGeometry(QtCore.QRect(50, 80, 341, 31))
            self.label_4.setObjectName("label_4")
            self.toolButton = QtWidgets.QToolButton(Dialog)
            self.toolButton.setGeometry(QtCore.QRect(360, 9, 25, 22))
            self.toolButton.setObjectName("toolButton")
            self.toolButton_2 = QtWidgets.QToolButton(Dialog)
            self.toolButton_2.setGeometry(QtCore.QRect(360, 59, 25, 22))
            self.toolButton_2.setObjectName("toolButton_2")
            self.label_5 = QtWidgets.QLabel(Dialog)
            self.label_5.setGeometry(QtCore.QRect(140, 106, 341, 31))
            self.label_5.setObjectName("label_5")
            self.pushButton_2 = QtWidgets.QPushButton(Dialog)
            self.pushButton_2.setGeometry(QtCore.QRect(300, 110, 75, 23))
            self.pushButton_2.setObjectName("pushButton_2")
            self.toolButton.clicked.connect(self.buttonClicked)
            self.toolButton_2.clicked.connect(self.buttonClicked2)
            self.pushButton.clicked.connect(self.buttonClicked3)
            self.pushButton_2.clicked.connect(self.save_to_file)
    
            self.retranslateUi(Dialog)
            QtCore.QMetaObject.connectSlotsByName(Dialog)
        def buttonClicked(self):
            szFile = QtWidgets.QFileDialog.getOpenFileName()[0]
    
            self.lineEdit.setText(szFile)
        def buttonClicked2(self):
            szFile = QtWidgets.QFileDialog.getOpenFileName()[0]
    
            self.lineEdit_2.setText(szFile)
        def buttonClicked3(self):
            if self.lineEdit.text()=="":
                print("notinfo")
            elif self.lineEdit_2.text()!="":
                one_file=get_hash_md5(self.lineEdit.text())
                two_file=get_hash_md5(self.lineEdit_2.text())
                self.label_3.setText(one_file)
                self.label_4.setText(two_file)
                is_savefile=1
                if one_file==two_file:
                    self.label_5.setText("Хеш одинаковый!")
                else:
                    self.label_5.setText("Хеш разный!")
                
    
        def save_to_file(self):
            if self.label_4.text()!="Hash":
                one_file=self.label_3.text()
                two_file=self.label_4.text()
                my_file = open("hash.txt", "w")
                my_file.write(self.lineEdit.text()+" hash: "+one_file+"\n")
                my_file.write(self.lineEdit_2.text()+" hash: "+two_file+"\n")
                my_file.close()
    
        def retranslateUi(self, Dialog):
            _translate = QtCore.QCoreApplication.translate
            Dialog.setWindowTitle(_translate("Dialog", "Сравнение хеша"))
            Dialog.setWindowIcon(QIcon('icon.ico'))
            self.pushButton.setText(_translate("Dialog", "Сравнить"))
            self.label.setText(_translate("Dialog", "<html><head/><body><p><span style=\" font-size:12pt; font-weight:600;\">1 Файл</span></p></body></html>"))
            self.label_2.setText(_translate("Dialog", "<html><head/><body><p><span style=\" font-size:12pt; font-weight:600;\">2 Файл</span></p></body></html>"))
            self.label_3.setText(_translate("Dialog", "<html><head/><body><p><span style=\" font-size:12pt; font-weight:600;\">Hash</span></p></body></html>"))
            self.label_4.setText(_translate("Dialog", "<html><head/><body><p><span style=\" font-size:12pt; font-weight:600;\">Hash</span></p></body></html>"))
            self.toolButton.setText(_translate("Dialog", "..."))
            self.toolButton_2.setText(_translate("Dialog", "..."))
            self.label_5.setText(_translate("Dialog", "<html><head/><body><p><span style=\" font-size:12pt; font-weight:600;\">Итог</span></p></body></html>"))
            self.pushButton_2.setText(_translate("Dialog", "Сохранить"))
    
    
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
- Tutorial: https://pythonprogramminglanguage.com/

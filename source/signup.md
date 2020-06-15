---
title: signup
date: 2020-05-07
---
Example Python program signup.py
This program creates a PyQt GUI

## Modules

* from PyQt5.Qt import *
* import socket
* from PyQt5.QtCore import *
* import time
* import sys

## Classes

* class Ui_signUp(object):
* class Dialog(QDialog):

## Methods

* def setupUi(self, Dialog):
* def retranslateUi(self, Dialog):
* def __init__(self, s, parent=None):
* def showMessageBox(self,arg):
* def insertData(self):

## Code

Example Python PyQt program :

    from PyQt5.Qt import *
    import socket
    from PyQt5.QtCore import *
    import time
    class Ui_signUp(object):
        def setupUi(self, Dialog):
            Dialog.setObjectName("Dialog")
            Dialog.resize(570, 375)
            self.label = QLabel(Dialog)
            self.label.setGeometry(QRect(160, 130, 81, 31))
            font = QFont()
            font.setPointSize(10)
            self.label.setFont(font)
            self.label.setObjectName("label")
            self.label_2 = QLabel(Dialog)
            self.label_2.setGeometry(QRect(160, 170, 81, 31))
            font = QFont()
            font.setPointSize(10)
            self.label_2.setFont(font)
            self.label_2.setObjectName("label_2")
            self.label_3 = QLabel(Dialog)
            self.label_3.setGeometry(QRect(150, 90, 350, 40))
            font = QFont()
            font.setPointSize(10)
            self.label_3.setFont(font)
            self.label_3.setObjectName("label_3")
            self.uname_lineEdit = QLineEdit(Dialog)
            self.uname_lineEdit.setGeometry(QRect(250, 130, 141, 20))
            self.uname_lineEdit.setObjectName("uname_lineEdit")
            self.password_lineEdit = QLineEdit(Dialog)
            self.password_lineEdit.setGeometry(QRect(250, 170, 141, 20))
            self.password_lineEdit.setObjectName("password_lineEdit")
            self.signup_btn = QPushButton(Dialog)
            self.signup_btn.setGeometry(QRect(270, 290, 75, 23))
            self.signup_btn.setObjectName("signup_btn")
            self.label_4 = QLabel(Dialog)
            self.label_4.setGeometry(QRect(150, 10, 321, 81))
            font = QFont()
            font.setPointSize(18)
            self.label_4.setFont(font)
            self.label_4.setAlignment(Qt.AlignCenter)
            self.label_4.setObjectName("label_4")
            self.retranslateUi(Dialog)
            QMetaObject.connectSlotsByName(Dialog)
        def retranslateUi(self, Dialog):
            _translate = QCoreApplication.translate
            Dialog.setWindowTitle(_translate("Dialog", "Dialog"))
            self.label.setText(_translate("Dialog", "USERNAME"))
            self.label_2.setText(_translate("Dialog", "PASSWORD"))
            self.signup_btn.setText(_translate("Dialog", "Sign Up"))
            self.label_4.setText(_translate("Dialog", "Create Account"))
    class Dialog(QDialog):
        def __init__(self, s, parent=None):
            super(Dialog, self).__init__(parent)
            self.ui = Ui_signUp()
            self.ui.setupUi(self)
            self.parent = parent
            self.host = '10.11.12.110'
            self.port = 8080
            self.message = b'no'
            self.s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
            self.s.connect((self.host,self.port))
            self.ui.signup_btn.clicked.connect(self.insertData)
        def showMessageBox(self,arg):
            _translate = QCoreApplication.translate
            self.ui.label_3.setText(_translate("MainWindow", arg))
            self.ui.label_3.setStyleSheet('color: red')
        def insertData(self):
            username = self.ui.uname_lineEdit.text()
            password = self.ui.password_lineEdit.text()
            if (not username) or (not password):
                self.ui.label_3.setGeometry(QRect(225, 90, 350, 40))
                msg = self.showMessageBox('Вы заполнили не все поля.')
                return
            self.s.send(("reg " + " name: " + username + " password: " + password).encode('utf-8'))
            time.sleep(2)
            if "зарегистрирован!" in self.s.recv(1024).decode('utf-8').split() :
                self.hide()
            else:
                self.ui.label_3.setGeometry(QRect(150, 90, 350, 40))
                msg = self.showMessageBox('Пользоватеть с таким именем уже зарегистрирован.')
    if __name__ == "__main__":
        import sys
        app    = QApplication(sys.argv)
        w = Dialog()
        w.show()
        sys.exit(app.exec_())

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/

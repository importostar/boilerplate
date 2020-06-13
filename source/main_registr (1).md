---
title: main_registr (1)
date: 2020-05-07
---
Example Python program main_registr (1).py
This program creates a PyQt GUI
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* from registr_window import Ui_MainWindow
* from PyQt5.QtWidgets import *
* from PyQt5.QtCore import *
* from PyQt5.QtGui import *
* import sys, socket
* from unt import messenger_
* from signup import Dialog
* from welcome import MainWindow

## Classes

* class MainDialog(QMainWindow):

## Methods

* def __init__(self, parent=None):
* def showMessageBox(self, arg):
* def welcomeWindowShow(self, username):
* def signUpShow(self):
* def loginCheck(self):
* def signUpCheck(self):
* def main():

## Code

Example Python PyQt program :

    from registr_window import Ui_MainWindow
    from PyQt5.QtWidgets import *
    from PyQt5.QtCore import *
    from PyQt5.QtGui import *
    import sys, socket
    from unt import messenger_
    from signup import Dialog
    from welcome import MainWindow
    
    
    class MainDialog(QMainWindow):
        def __init__(self, parent=None):
            super(MainDialog, self).__init__(parent)
            self.ui = Ui_MainWindow()
            self.ui.setupUi(self)
            self.host = '10.11.12.110'
            self.port = 8080
            self.message = b'no'
            self.s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
            self.s.connect((self.host, self.port))
            self.ui.Button_login.clicked.connect(self.loginCheck)
            self.ui.Button_registr.clicked.connect(self.signUpCheck)
    
        def showMessageBox(self, arg):
            _translate = QCoreApplication.translate
            self.ui.label_4.setText(_translate("MainWindow", arg))
            self.ui.label_4.setStyleSheet('color: red')
    
        def welcomeWindowShow(self, username):
            self.main_window = messenger_(self.username)
            self.main_window.show()
    
        def signUpShow(self):
            self.signUpWindow = Dialog(self, self.s)
            self.signUpWindow.show()
    
        def loginCheck(self):
            print("plus")
            self.username = self.ui.lineEdit.text()
            self.password = self.ui.lineEdit_2.text()
    
            if (not self.username) or (not self.password):
                self.showMessageBox("заполнены не все поля!")
                return
            else:
                print(self.username + " " + self.password)
            self.s.send(("log" + " login: " + self.username + " password: " + self.password).encode('utf-8'))
            self.data = self.s.recv(1024).decode('utf-8').split()
            print(self.data)
            if "выполнен!" in self.data:
                self.welcomeWindowShow(self.username)
                self.hide()
                self.s.close()
            else:
                self.showMessageBox('Неправильное имя пользователя или пароль.')
    
        def signUpCheck(self):
            print("minus")
            self.signUpShow()
    
    
    def main():
        app = QApplication(sys.argv)
        window = MainDialog()
        window.show()
        app.exec_()
    
    
    if __name__ == '__main__':
        main()
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/

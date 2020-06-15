---
title: chat
date: 2020-05-07
---
Example Python program chat.py
This program creates a PyQt GUI

## Modules

* from PyQt5 import QtWidgets, QtCore
* import clientui
* import requests
* from datetime import datetime
* from PyQt5 import QtCore, QtGui, QtWidgets

## Classes

* class ChatWindow(QtWidgets.QMainWindow, clientui.Ui_MainWindow):
* class Ui_MainWindow(object):

## Methods

* def __init__(self):
* def sendMessage(self):
* def addText(self, text):
* def getUpdates(self):
* def setupUi(self, MainWindow):
* def retranslateUi(self, MainWindow):

## Code

Example Python PyQt program :

    from PyQt5 import QtWidgets, QtCore
    import clientui
    import requests
    from datetime import datetime
    
    class ChatWindow(QtWidgets.QMainWindow, clientui.Ui_MainWindow):
        def __init__(self):
            super().__init__()
            self.setupUi(self)
            self.pushButton.pressed.connect(self.sendMessage)
            self.last_message_time = 0
            self.timer = QtCore.QTimer()
            self.timer.timeout.connect(self.getUpdates)
            self.timer.start(1000)
    
        def sendMessage(self):
            username = self.lineEdit.text()
            password = self.lineEdit_2.text()
            text = self.textEdit.toPlainText()
    
            if not username:
                self.addText('ERROR: Не указано имя пользователя')
                self.addText('')
                return
            if not password:
                self.addText('ERROR: Не указан пароль')
                self.addText('')
                return
            if not text:
                self.addText('ERROR: Не указан текст сообщения')
                self.addText('')
                return
    
            response = requests.post('http://127.0.0.1:5000/send',
                                     json={'username': username, 'password': password, 'text': text})
    
            if not response.json()['ok']:
                self.addText('ERROR: Нет доступа, вы указали неверный пароль')
                self.addText('')
                return
    
            self.textEdit.clear()
            self.textEdit.repaint()
    
    
        def addText(self, text):
            self.textBrowser.append(text)
            self.textBrowser.repaint()
    
        def getUpdates(self):
            response = requests.get(
                'http://127.0.0.1:5000/history',
                params={'after': self.last_message_time}
            )
            data = response.json()
            for message in data['messages']:
                beauty_time = datetime.fromtimestamp(message['time'])
                beauty_time = beauty_time.strftime("%d/%m/%Y %H:%M:%S")
                self.addText(beauty_time + '       ' + message['username'])
                self.addText(message['text'])
                self.addText('')
                self.last_message_time = message["time"]
    
    
    
    
    
    
    app = QtWidgets.QApplication([])
    window = ChatWindow()
    window.show()
    app.exec_()
    
    
    
    
    #второй файл с графическим интерфейсом
    # -*- coding: utf-8 -*-
    
    # Form implementation generated from reading ui file 'chat.ui'
    #
    # Created by: PyQt5 UI code generator 5.14.1
    #
    # WARNING! All changes made in this file will be lost!
    
    
    from PyQt5 import QtCore, QtGui, QtWidgets
    
    
    class Ui_MainWindow(object):
        def setupUi(self, MainWindow):
            MainWindow.setObjectName("MainWindow")
            MainWindow.resize(372, 587)
            self.centralwidget = QtWidgets.QWidget(MainWindow)
            self.centralwidget.setObjectName("centralwidget")
            self.label = QtWidgets.QLabel(self.centralwidget)
            self.label.setGeometry(QtCore.QRect(100, 10, 171, 41))
            font = QtGui.QFont()
            font.setFamily("OCR A Extended")
            font.setPointSize(28)
            self.label.setFont(font)
            self.label.setObjectName("label")
            self.textBrowser = QtWidgets.QTextBrowser(self.centralwidget)
            self.textBrowser.setGeometry(QtCore.QRect(10, 120, 351, 331))
            self.textBrowser.setObjectName("textBrowser")
            self.textEdit = QtWidgets.QTextEdit(self.centralwidget)
            self.textEdit.setGeometry(QtCore.QRect(10, 460, 351, 61))
            self.textEdit.setObjectName("textEdit")
            self.pushButton = QtWidgets.QPushButton(self.centralwidget)
            self.pushButton.setGeometry(QtCore.QRect(10, 530, 351, 31))
            self.pushButton.setAutoFillBackground(False)
            self.pushButton.setObjectName("pushButton")
            self.lineEdit = QtWidgets.QLineEdit(self.centralwidget)
            self.lineEdit.setGeometry(QtCore.QRect(150, 60, 211, 20))
            self.lineEdit.setObjectName("lineEdit")
            self.lineEdit_2 = QtWidgets.QLineEdit(self.centralwidget)
            self.lineEdit_2.setGeometry(QtCore.QRect(150, 90, 211, 20))
            self.lineEdit_2.setObjectName("lineEdit_2")
            self.label_2 = QtWidgets.QLabel(self.centralwidget)
            self.label_2.setGeometry(QtCore.QRect(10, 60, 141, 20))
            font = QtGui.QFont()
            font.setPointSize(11)
            self.label_2.setFont(font)
            self.label_2.setObjectName("label_2")
            self.label_3 = QtWidgets.QLabel(self.centralwidget)
            self.label_3.setGeometry(QtCore.QRect(10, 90, 141, 20))
            font = QtGui.QFont()
            font.setPointSize(11)
            self.label_3.setFont(font)
            self.label_3.setObjectName("label_3")
            MainWindow.setCentralWidget(self.centralwidget)
            self.statusbar = QtWidgets.QStatusBar(MainWindow)
            self.statusbar.setObjectName("statusbar")
            MainWindow.setStatusBar(self.statusbar)
    
            self.retranslateUi(MainWindow)
            QtCore.QMetaObject.connectSlotsByName(MainWindow)
    
        def retranslateUi(self, MainWindow):
            _translate = QtCore.QCoreApplication.translate
            MainWindow.setWindowTitle(_translate("MainWindow", "My Chat"))
            self.label.setText(_translate("MainWindow", "My CHAT"))
            self.pushButton.setText(_translate("MainWindow", "Отправить"))
            self.label_2.setText(_translate("MainWindow", "Имя пользователя:"))
            self.label_3.setText(_translate("MainWindow", "Пароль:"))
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/

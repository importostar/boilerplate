---
title: unt
date: 2020-05-07
---
Example Python program unt.py
This program creates a PyQt GUI
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* from PyQt5 import QtCore, QtGui, QtWidgets
* from PyQt5.Qt import *
* from PyQt5.QtWidgets import *
* from PyQt5.QtCore import *
* from PyQt5.QtGui import *
* import socket
* import threading
* from desi import Ui_MainWindow
* import sqlite3
* from dialog import Ui_Form
* import pickle
* import sys

## Classes

* class messenger_(QMainWindow):

## Methods

* def __init__(self, username, parent=None):
* def handler(self):
* def receive(self, s, a):
* def clicked_but(self):
* def find(self):
* def addInGroup(self,event):
* def contextMenuEvent(self, event):
* def nado(self):
* def get_key(self,d):
* def receiv(self):
* def pressedKeys(self):
* def listview(self):

## Code

Example Python PyQt program :

    from PyQt5 import QtCore, QtGui, QtWidgets
    from PyQt5.Qt import *
    from PyQt5.QtWidgets import *
    from PyQt5.QtCore import *
    from PyQt5.QtGui import *
    import socket
    import threading
    from desi import Ui_MainWindow
    import sqlite3
    from dialog import Ui_Form
    import pickle
    
    class messenger_(QMainWindow):
        def __init__(self, username, parent=None):
            super(messenger_, self).__init__(parent)
            
            self.ui = Ui_MainWindow()
            self.ui.setupUi(self)
            self.con = sqlite3.connect("messages.db",check_same_thread = False)
            self.c = self.con.cursor()
            self.username = username
            self.host = '10.11.12.110'
            self.port = 60005
            self.s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
            self.s.connect((self.host, self.port))
            self.s.send(("name: " + self.username).encode('utf-8'))
            self.pixmap = QPixmap("C:\\Users\\Admin2\\Desktop\\Python Files\\detection\\tutor\\servers\\3.jpg")
            self.ui.label.setMaximumSize(100, 100)
            self.ui.label.setPixmap(self.pixmap)
            self.ui.label.setScaledContents(True)
            self.ui.label_2.setText(self.username)
            self.thread = threading.Thread(target=self.find)
            self.thread.start()
            self.handler()
            self.thread_1 = threading.Thread(target=self.receive, args=(self.s, "a"))
            self.thread_1.start()
        def handler(self):
            self.ui.pushButton.clicked.connect(self.clicked_but)
        def receive(self, s, a):
            while True:
                self.data = self.s.recv(2048)
                data = self.data.decode('utf-8').split()
                print(data)
                m = data.index('message:')
                sender = ' '.join(data[0:m])
                message_ = ' '.join(data[m+1:])
                self.c.execute("""CREATE TABLE IF NOT EXISTS """ + '"' + sender + '"' + """(sender TEXT, message TEXT)""")
                self.c.execute("""INSERT INTO""" + '"' + sender + '"' + """VALUES (?,?)""", (sender, message_,))
                self.con.commit()
                print(sender, message_)
                _translate = QtCore.QCoreApplication.translate
                if self.ui.listWidget.count()>0:
                    for self.item in range(self.ui.listWidget.count()): 
                        print(self.item)
                        if self.ui.listWidget.item(self.item).text() == sender: 
                            print("if")
                            brush = QtGui.QBrush(QtGui.QColor(166, 226, 43))
                            brush.setStyle(QtCore.Qt.SolidPattern)
                            itemm = self.ui.listWidget.item(self.item)
                            itemm.setBackground(brush)
                            print(itemm.text())
                        else:
                            print("No")
                            self.ui.listWidget.addItem(sender)
                            brush = QtGui.QBrush(QtGui.QColor(166, 226, 43))
                            brush.setStyle(QtCore.Qt.SolidPattern)
                            itemm = self.ui.listWidget.item(self.item)
                            itemm.setBackground(brush)
                            print(itemm.text())
                else:
                    self.ui.listWidget.addItem(sender)
                    brush = QtGui.QBrush(QtGui.QColor(166, 226, 43))
                    brush.setStyle(QtCore.Qt.SolidPattern)
                    itemm = self.ui.listWidget.item(0)
                    itemm.setBackground(brush)
                    print(itemm.text())
                #self.guest_message = str('Received from ' + sender +': '+ message_)
                #self.ui.plainTextEdit.appendPlainText(self.guest_message)
        def clicked_but(self):
            self.msg = self.ui.plainTextEdit_2.toPlainText().split()
            print(self.msg)
            self.message = self.msg[0:]
            self.message = ' '.join(self.message)
            self.ui.plainTextEdit.appendPlainText(self.message)
            self.c.execute("""INSERT INTO""" + '"' + self.item + '"' + """VALUES (?,?)""", (self.username, self.message,))
            self.con.commit()
            self.s.send(("sender: " + self.username + " receiver: " + self.item + " message: " + self.message).encode('utf-8')) 
            self.ui.plainTextEdit_2.clear()
        def find(self):
            host = '10.11.12.110'
            port = 8888
            self.sock = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
            self.sock.connect((host, port))
            self.sock.send(("name: " + self.username).encode('utf-8'))
            self.new_thread = threading.Thread(target=self.receiv)
            self.new_thread.start()
            self.line = self.ui.comboBox.lineEdit()
            self.ui.listWidget.itemClicked.connect(self.listview)
            self.line.returnPressed.connect(self.nado)
        def addInGroup(self,event):
            self.menu_1 = QMenu(self)
            self.ui.listWidget.setSelectionMode(QAbstractItemView.MultiSelection)
            for x in range(0,self.ui.listWidget.count()):
                action = self.menu_1.addAction(self.ui.listWidget.item(x).text())
            result = self.menu_1.exec_(self.mapToGlobal(event.pos()))
            
        def contextMenuEvent(self, event):
            self.menu = QMenu(self)
            action = self.menu.addAction("Добавить в группу")
            action_1 = self.menu.addAction("press")
            result = self.menu.exec_(self.mapToGlobal(event.pos()))
            if action == result:
                self.addInGroup(event)
            elif action_1 == result:
                print("press")    
        def nado(self):
            self.sock.send((self.line.text()).encode('utf-8'))
            print("send")
            self.ui.comboBox.hidePopup()
            self.ui.comboBox.clear()
            #self.ui.listWidget.takeItem(self.ui.listWidget.selectedItems()[0])
            self.ui.comboBox.activated.connect(self.pressedKeys)
        def get_key(self,d):
            for item in d.items():
                print(item[0], item[1])
                f = open(item[0] +".png",'wb')
                f.write(item[1])
                f.close()
                icon = QtGui.QIcon()
                icon.addPixmap(QtGui.QPixmap(item[0] + ".png"), QtGui.QIcon.Normal, QtGui.QIcon.Off)
                self.ui.comboBox.addItem(icon, item[0])
        def receiv(self):
            while True:
                self.dataa = self.sock.recv(40960000)#.decode('utf-8').split(",")
                self.dataa = pickle.loads(self.dataa)
                print(self.dataa)
                if self.dataa:
                    self.get_key((self.dataa))
        def pressedKeys(self):
            self.ui.listWidget.setIconSize(QtCore.QSize(40, 40))
            self.current_item = self.ui.comboBox.currentText()
            print(self.current_item)
            item = QtWidgets.QListWidgetItem()
            icon = QtGui.QIcon()
            icon.addPixmap(QtGui.QPixmap(self.current_item +".png"), QtGui.QIcon.Normal, QtGui.QIcon.Off)
            item.setIcon(icon)
            item.setText(self.current_item)
            self.ui.listWidget.addItem(item)
            self.ui.comboBox.activated.disconnect(self.pressedKeys)
        def listview(self):
            self.ui.plainTextEdit.clear()
            brush = QtGui.QBrush(QtGui.QColor(255, 225, 255))
            brush.setStyle(QtCore.Qt.SolidPattern)
            itemm = self.ui.listWidget.currentItem()
            itemm.setBackground(brush)
            self.item = self.ui.listWidget.currentItem().text()
            self.c.execute("""CREATE TABLE IF NOT EXISTS """ + '"' + self.item + '"' + """(sender TEXT, message TEXT)""")
            self.c.execute("""SELECT * FROM """'"'+ self.item + '"')
            f = self.c.fetchall()
            if f is not None:
                for x in range(0, len(f)):
                    mess = f[x][1:]
                    mess = ".".join(mess)
                    self.ui.plainTextEdit.appendPlainText(f[x][0] + " : " + mess)
            print(self.item)
    if __name__ == "__main__":
        import sys
        app = QApplication(sys.argv)
        w = messenger_()
        w.show()
        sys.exit(app.exec_())

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/

---
title: Client
date: 2020-05-07
---
Example Python program Client.py
This program creates a PyQt GUI
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import socket
* import sys
* import time
* from PyQt5 import QtCore, QtGui, QtWidgets
* from PyQt5.QtCore import QThread
* from klient_gui import Ui_MainWindow

## Classes

* class MyForm(QtWidgets.QMainWindow):
* class Polaczenie(QtCore.QThread):

## Methods

* def __init__(self, parent=None):
* def updateLCD(self):
* def start_linczik(self, b):
* def __init__(self, parent):
* def run(self):
* def event_dispatcher(self, a, b):

## Code

Example Python PyQt program :

    import socket
    import sys
    import time
    
    from PyQt5 import QtCore, QtGui, QtWidgets
    from PyQt5.QtCore import QThread
    
    from klient_gui import Ui_MainWindow
    
    
    class MyForm(QtWidgets.QMainWindow):
        def __init__(self, parent=None):
            QtWidgets.QWidget.__init__(self, parent)
            self.ui = Ui_MainWindow()
            self.ui.setupUi(self)
            # Pelen ekran
            # self.showFullScreen()
            self.showMaximized()
            self.timer = QtCore.QTimer(self)
            self.polaczenie = Polaczenie(self)
            self.polaczenie.start()
            #self.start_linczik(20)
    
        @QtCore.pyqtSlot()
        def updateLCD(self):
            # Update the lcd
            self.start_time -= 1
            if self.start_time >= 0:
                self.ui.lcdNumber.display("%d:%02d" % (self.start_time / 60, self.start_time % 60))
            else:
                self.timer.stop()
    
        @QtCore.pyqtSlot(int)
        def start_linczik(self, b):
            self.start_time = b
            self.ui.lcdNumber.display("%d:%02d" % (self.start_time / 60, self.start_time % 60))
            self.timer.start(1000)
            self.timer.timeout.connect(self.updateLCD)
    
    class Polaczenie(QtCore.QThread):
        sig = QtCore.pyqtSignal(str,str)
        def __init__(self, parent):
            super(Polaczenie, self).__init__(parent)
            self.sig.connect(self.event_dispatcher)
    
        def run(self):
            server = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
            ip = "127.0.0.1"
            port = 1234
            adress = (ip, port)
            server.bind(adress)
            server.listen(1)
    
            while True:
                print("Start listenint on ", ip, " on ", port)
                (client, addr) = server.accept()
                print("Got connection from ", addr[0], ":", addr[1])
                data = client.recv(1024)
                data = data.decode()
                print("Recived ", data, " from the client")
                print("Processin data")
                indeks_srednik = data.index(";")
                instrukcja = data[:indeks_srednik]
                try:
                    string = data[indeks_srednik+1:]
                except Exception as e:
                    print(e)
                try:
                    print(instrukcja)
                    print(string)
                    if instrukcja == "zamknij":
                        # Zamykanie aplikacji przy pomocy serwera
                        server.close()
                        sys.exit(0)
                    elif instrukcja == "czas_set":
                        self.sig.emit("czas_set", string)
                except Exception as e:
                    print(e)
    
        def event_dispatcher(self, a, b):
            # funkcja dispatchujaca eventy
            if a == "czas_set":
                print("licznik start")
                print(a)
                print(b)
                b=int(b)
                #MyForm().start_linczik(b)
                QtCore.QMetaObject.invokeMethod(self.parent(), "start_linczik", 
                    QtCore.Qt.QueuedConnection,  QtCore.Q_ARG(int, b))
    
    
    if __name__ == "__main__":
        app = QtWidgets.QApplication(sys.argv)
        myapp = MyForm()
        myapp.show()
        sys.exit(app.exec_())

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/

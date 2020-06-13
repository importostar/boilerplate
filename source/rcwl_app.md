---
title: rcwl_app
date: 2020-05-07
---
Example Python program rcwl_app.py
This program creates a PyQt GUI
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* from PyQt5 import QtCore, QtSerialPort
* from PyQt5.QtWidgets import *
* from PyQt5.QtCore import *
* from PyQt5.QtGui import *
* from PyQt5.QtWebEngineWidgets import *
* import sys
* import sys

## Classes

* class Color(QWidget):
* class MainWindow(QMainWindow):

## Methods

* def __init__(self, color, *args, **kwargs):
* def set_color(self, color):
* def __init__(self, *args, **kwargs):
* def receive(self):
* def on_toggled(self, checked):

## Code

Example Python PyQt program :

    
    from PyQt5 import QtCore, QtSerialPort
    from PyQt5.QtWidgets import *
    from PyQt5.QtCore import *
    from PyQt5.QtGui import *
    from PyQt5.QtWebEngineWidgets import *
    
    # Only needed for access to command line arguments
    import sys
    
    class Color(QWidget):
    
        def __init__(self, color, *args, **kwargs):
            super(Color, self).__init__(*args, **kwargs)
            self.setAutoFillBackground(True)
            
            palette = self.palette()
            palette.setColor(QPalette.Window, QColor(color))
            self.setPalette(palette)
        def set_color(self, color):
            palette = self.palette()
    
            palette.setColor(QPalette.Window, QColor(color))
            self.setPalette(palette)
    
    
    # Subclass QMainWindow to customise your application's main window
    class MainWindow(QMainWindow):
    
        def __init__(self, *args, **kwargs):
            super(MainWindow, self).__init__(*args, **kwargs)
            
            self.setWindowTitle("RCWL APP")
    
            layout1 = QVBoxLayout()
            layout2 = QHBoxLayout()
    
            self.connect_btn = QPushButton(
                text="Connect",
                checkable=True,
                clicked=self.on_toggled
            )
    
            self.output_te = QTextEdit(readOnly=True)
            
            self.outputLabel = QLabel("Hi there!")
            self.setStyleSheet("QLabel {font: 30pt Comic Sans MS}")
            self.color = Color("grey")
            self.color.setMinimumHeight(30)
    
            self.view = QWebEngineView()
            self.view.setHtml('''
              <html>
                <style type="text/css">
                    .iframe-container {
                      overflow: hidden;
                      padding-top: 56.25%;
                      position: relative;
                    }
                     
                    .iframe-container iframe {
                       border: 0;
                       height: 100%;
                       left: 0;
                       position: absolute;
                       top: 0;
                       width: 100%;
                    }
                     
                    /* 4x3 Aspect Ratio */
                    .iframe-container-4x3 {
                      padding-top: 75%;
                    }
                </style>
                <body>
                    <div class="iframe-container">
                        <iframe src="http://192.168.1.119/"></iframe>
                    </div>
                </body>
    
              </html>
            ''')
     
            layout1.addWidget(self.connect_btn)
            layout1.addWidget(self.output_te)
            layout2.addWidget(self.outputLabel)
            layout2.addWidget(self.color)
            layout1.addLayout(layout2)
            layout1.addWidget(self.view)
    
            
            widget = QWidget()
            widget.setLayout(layout1)
            self.setCentralWidget(widget)
            self.serial = QtSerialPort.QSerialPort(
                app.arguments()[1],
                baudRate=QtSerialPort.QSerialPort.Baud9600,
                readyRead=self.receive
            )
    
        @QtCore.pyqtSlot()
        def receive(self):
            while self.serial.canReadLine():
                try:
                    text = self.serial.read(1).decode()
                    text = self.serial.read(1).decode()
                    text = text.rstrip('\r\n')
                    if bool(text):
                        self.output_te.append(text)
                        self.outputLabel.setText("Motion detected" if text == "1" else "Waiting...")
                        self.color.set_color("red"if text == "1" else "grey")
                except UnicodeDecodeError:
                    # fall back to latin1 in case the message isn't valid utf-8
                    next
    
        @QtCore.pyqtSlot(bool)
        def on_toggled(self, checked):
            self.connect_btn.setText("Disconnect" if checked else "Connect")
            if checked:
                if not self.serial.isOpen():
                    print("1")
                    if not self.serial.open(QtCore.QIODevice.ReadWrite):
                        print("2")
                        self.connect_btn.setChecked(False)
                    else:
                        print(self.serial.read(1))
            else:
                self.outputLabel.setText("Hi there!")
                self.color.set_color("grey")
                self.serial.close()
    
    
    
    if __name__ == '__main__':
        import sys
        if (len(sys.argv) != 2):
            print("command line: rcwl_monitor.py serial_port")
            sys.exit()
        app = QApplication(sys.argv)
        window = MainWindow()
        window.show()
        sys.exit(app.exec_())
    
    
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/

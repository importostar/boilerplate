---
title: taskbar2
date: 2020-05-07
---
Example Python program taskbar2.py
This program creates a PyQt GUI
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import sys
* from PyQt5.QtWidgets import QApplication, QWidget, QDesktopWidget
* from PyQt5.QtGui import QIcon
* from PyQt5.QtWidgets import QHBoxLayout
* from PyQt5.QtWidgets import QLabel
* from PyQt5.QtWidgets import QLineEdit
* from PyQt5.QtWidgets import QListWidget
* from PyQt5.QtWidgets import QMainWindow
* from PyQt5.QtWidgets import QPushButton
* from PyQt5 import QtCore
* from PyQt5.QtWidgets import QVBoxLayout

## Classes

* class Example(QWidget):
* class myListWidget(QListWidget):

## Methods

* def __init__(self):
* def initUI(self):
* def execute(self):
* def center(self):
* def onChanged(self, text):
* def keyPressEvent(self, e):
*    def Clicked(self,item):

## Code

Example Python PyQt program :

    import sys
    
    from PyQt5.QtWidgets import QApplication, QWidget, QDesktopWidget
    from PyQt5.QtGui import QIcon
    from PyQt5.QtWidgets import QHBoxLayout
    from PyQt5.QtWidgets import QLabel
    from PyQt5.QtWidgets import QLineEdit
    from PyQt5.QtWidgets import QListWidget
    from PyQt5.QtWidgets import QMainWindow
    from PyQt5.QtWidgets import QPushButton
    from PyQt5 import QtCore
    from PyQt5.QtWidgets import QVBoxLayout
    
    
    class Example(QWidget):
        def __init__(self):
            super().__init__()
    
            self.initUI()
    
        def initUI(self):
            x = 300
            y = 300
            height = 150
            width = 300
            self.setGeometry(x, y, width, height)
            self.setWindowTitle('Icon')
            self.setWindowIcon(QIcon('Twitter-50.png'))
            self.center()
            btn = QPushButton('Go', self)
            self.lbl = QLabel(self)
            self.qle = QLineEdit(self)
    
            hbox = QHBoxLayout()
            hbox.addWidget(self.qle)
            hbox.addWidget(btn)
            vbox = QVBoxLayout()
            vbox.addLayout(hbox)
            self.setLayout(vbox)
            btn.pressed.connect(self.execute)
            self.qle.textChanged[str].connect(self.onChanged)
            self.qle.returnPressed.connect(self.execute)
            self.setWindowFlags(QtCore.Qt.FramelessWindowHint
                          | QtCore.Qt.Window
                          | QtCore.Qt.WindowSystemMenuHint
    
                          )
    
            self.show()
    
        def execute(self):
            print(self.qle.text())
    
        def center(self):
            qr = self.frameGeometry()
            cp = QDesktopWidget().availableGeometry().center()
            qr.moveCenter(cp)
            self.move(qr.topLeft())
    
        def onChanged(self, text):
            pass
    
        def keyPressEvent(self, e):
            if e.key() == QtCore.Qt.Key_Escape:
                self.close()
    
    class myListWidget(QListWidget):
    
       def Clicked(self,item):
          QMessageBox.information(self, "ListWidget", "You clicked: "+item.text())
    
    if __name__ == '__main__':
    
        app = QApplication(sys.argv)
        ex = Example()
        sys.exit(app.exec_())

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/

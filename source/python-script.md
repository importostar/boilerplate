---
title: python script
date: 2020-05-07
---
Example Python program python-script.py
This program creates a PyQt GUI
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import sys
* from PyQt5.QtWidgets import (QWidget, QToolTip, QPushButton, QApplication)
* from PyQt5.QtGui import QFont
* from PyQt5.QtCore import pyqtSlot
* import subprocess
* import shutil
* from qtpy import QtWidgets, QtCore
* from QNotifications import QNotificationArea

## Classes

* class Example(QWidget):

## Methods

* def __init__(self):
* def on_click(self):
* def on_click_cache(self):
* def initUI(self):

## Code

Example Python PyQt program :

    #!/usr/bin/python3
    # -*- coding: utf-8 -*-
    import sys
    from PyQt5.QtWidgets import (QWidget, QToolTip, QPushButton, QApplication)
    from PyQt5.QtGui import QFont
    from PyQt5.QtCore import pyqtSlot
    import subprocess
    import shutil
    from qtpy import QtWidgets, QtCore
    from QNotifications import QNotificationArea
    
    class Example(QWidget):
    
        qna = QNotificationArea(QtWidgets.QWidget())
    
        def __init__(self):
            super(Example, self).__init__()
            self.initUI()
    
        @pyqtSlot()
        def on_click(self):
            print('PyQt5 button click')
            # subprocess.Popen(r'explorer /open,"C:\WB Resources\"')        
            qna.display('No Folder!', 'danger', 5000)
    
        def on_click_cache(self):
            path = "C:/Users/ischwartz/AppData/Local/Packages/Wellbeats.WELLBEATS_yh48yaajx8nst/LocalState/cacheddata/"
            try:
                shutil.rmtree(path)
            except:
                print('No folder')
                # Create a widget to render the notifications on.
                targetWidget = QtWidgets.QWidget()
                targetWidget.setGeometry(100, 100, 800, 600)
                # Create a new notification area, and pass it the target widget.
                qna = QNotificationArea(targetWidget)
                # Show the target widget.
                targetWidget.show()
    
                # Show a 'primary' styled notification for 1 second.
                qna.display('This is a primary notification', 'primary', 1000)
                # Show an 'info' styled notification for 2 seconds.
                qna.display('This is an info notification', 'info', 2000)
                # Show a 'danger' styled notification until the user closes it manually.
                qna.display('This is an error notification', 'danger', None)
    
            self.btn_clearcache.setStyleSheet("background-color: green")
    
        def initUI(self):
            QToolTip.setFont(QFont('SansSerif', 10))
    
            btn = QPushButton('Open WBR',self)
            btn.setToolTip('This is a <b>QPushButton</b> widget')
            btn.resize(150,50)
            btn.move(0, 0)
            btn.clicked.connect(self.on_click)
    
            self.btn_clearcache = QPushButton('Clear Cache', self)
            self.btn_clearcache.setToolTip('Clear the WB App Cache<br><b>THIS IS DESTRUCTIVE</b>')
            self.btn_clearcache.resize(150,50)
            self.btn_clearcache.move(151, 0)
            self.btn_clearcache.setStyleSheet("QPushButton:focus:pressed { background-color: red }")
            self.btn_clearcache.clicked.connect(self.on_click_cache)
            self.setGeometry(500, 350, 900, 500)
            self.setWindowTitle('WB-TOOL')
            qna = QNotificationArea(self)
            self.show()
    
    
    
    if __name__ == '__main__':
        app = QApplication(sys.argv)
        ex = Example()
        sys.exit(app.exec_())

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/

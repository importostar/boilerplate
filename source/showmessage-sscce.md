---
title: showmessage sscce
date: 2020-05-07
---
Example Python program showmessage-sscce.py
This program creates a PyQt GUI
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* from PyQt5 import QtCore
* from PyQt5 import QtGui
* from PyQt5 import QtWidgets
* import sys

## Classes

* class MyMainWindow(QtWidgets.QMainWindow):

## Methods

* def __init__(self):

## Code

Example Python PyQt program :

    
    from PyQt5 import QtCore
    from PyQt5 import QtGui
    from PyQt5 import QtWidgets
    
    import sys
    print('sys.version:', sys.version)
    print('sys.platform:', sys.platform)
    print('QT_VERSION_STR:', QtCore.QT_VERSION_STR)
    print('PYQT_VERSION_STR:', QtCore.PYQT_VERSION_STR)
    
    ICON_FILE_PATH_STR = "icon.png"
    
    class MyMainWindow(QtWidgets.QMainWindow):
        def __init__(self):
            super().__init__()
    
            self.tray_icon = QtWidgets.QSystemTrayIcon(QtGui.QIcon(ICON_FILE_PATH_STR), app)
            self.tray_icon.show()
    
    
            self.setGeometry(40, 30, 200, 200)
            self.setMaximumWidth(200)
    
    
            self.show()
    
    
            self.tray_icon.showMessage(
                "title",
                "this one works",
                QtWidgets.QSystemTrayIcon.Information  # -OK
            )
            self.tray_icon.showMessage(
                "title",
                "this one fails",
                QtGui.QIcon(ICON_FILE_PATH_STR)
            )
            #  -NOK, gives the following:
            """
            /usr/bin/python3.5 /home/sunyata/PycharmProjects/pyqt5-experiments/showmessage-sscce.py
            Traceback (most recent call last):
              File "/home/sunyata/PycharmProjects/pyqt5-experiments/showmessage-sscce.py", line 38, in <module>
                main_window = MyMainWindow()
              File "/home/sunyata/PycharmProjects/pyqt5-experiments/showmessage-sscce.py", line 28, in __init__
                QtGui.QIcon(ICON_FILE_PATH_STR)  # -OK
            TypeError: showMessage(self, str, str, icon: QSystemTrayIcon.MessageIcon = QSystemTrayIcon.Information, msecs: int = 10000): argument 3 has unexpected type 'QIcon'
            """
    
    
    app = QtWidgets.QApplication(sys.argv)
    main_window = MyMainWindow()
    main_window.show()
    app.exec_()
    
    
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/

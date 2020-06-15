---
title: pyqt qsettings
date: 2020-05-07
---
Example Python program pyqt-qsettings.py
This program creates a PyQt GUI
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* from PyQt5.QtWidgets import QApplication, QMainWindow
* from PyQt5.QtCore import QCoreApplication, QSettings
* import sys

## Classes

* class Window(QMainWindow):

## Methods

* def __init__(self):
* def closeEvent(self, event):

## Code

Example Python PyQt program :

    #! /usr/bin/python3
    
    from PyQt5.QtWidgets import QApplication, QMainWindow
    from PyQt5.QtCore import QCoreApplication, QSettings
    
    class Window(QMainWindow):
        def __init__(self):
            super(Window, self).__init__()
            settings = QSettings()
            self.list = settings.value('list', ['a', 'b', 'c'])
            self.dict = settings.value('dict', {'key': 0})
            self.str = settings.value('string', 'str')
            self.int = settings.value('interger', 0, int)
    
            print("list: ", self.list)
            print("dict: ", self.dict)
            print("string:", self.str)
            print("interger:", self.int)
    
            # Change value for testings
            self.list.append(len(self.list))
            self.str = self.str + str(len(self.list))
            self.int = self.int + 1
            self.dict[self.str] = self.int
    
        def closeEvent(self, event):
            settings = QSettings()
            settings.setValue('list', self.list)
            settings.setValue('dict', self.dict)
            settings.setValue('string', self.str)
            settings.setValue('interger', self.int)
    
    
    if __name__ == '__main__':
        QCoreApplication.setOrganizationName('org_name')
        QCoreApplication.setOrganizationDomain('org_domain')
        QCoreApplication.setApplicationName('app_name')
    
        import sys
        app = QApplication(sys.argv)
        window = Window()
        window.show()
        sys.exit(app.exec_())
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/

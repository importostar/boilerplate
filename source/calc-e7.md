---
title: calc e7
date: 2020-05-07
---
Example Python program calc-e7.py
This program creates a PyQt GUI

## Modules

* import sys
* from PyQt5.QtWidgets import QApplication
* from PyQt5.QtWidgets import QLabel
* from PyQt5.QtWidgets import QMainWindow  #主視窗
* from PyQt5.QtWidgets import QStatusBar  #狀態列
* from PyQt5.QtWidgets import QToolBar  #工具列

## Classes

* class Window(QMainWindow):  #繼承自QMainWindow

## Methods

* def __init__(self, parent=None):
* def _createMenu(self):
* def _createToolBar(self):
* def _createStatusBar(self):

## Code

Example Python PyQt program :

    import sys
    
    from PyQt5.QtWidgets import QApplication
    from PyQt5.QtWidgets import QLabel
    from PyQt5.QtWidgets import QMainWindow  #主視窗
    from PyQt5.QtWidgets import QStatusBar  #狀態列
    from PyQt5.QtWidgets import QToolBar  #工具列
    
    class Window(QMainWindow):  #繼承自QMainWindow
        #初始化
        def __init__(self, parent=None):
            super().__init__(parent)
            self.setWindowTitle('主視窗')
            self.setCentralWidget(QLabel("必備的中央部件"))  #CentralWidget縱使是空的，也要有一個。
            #內部的method，建立功能表、工具列和狀態列實體
            self._createMenu()
            self._createToolBar()
            self._createStatusBar()
        #定義3個class內部的private methods
        def _createMenu(self):
            self.menu = self.menuBar().addMenu("&Menu") #功能表新增Menu，及第一個字M是快速鍵，以後都相同。
            self.menu.addAction('&Exit', self.close) #Menu裡面的選項，在此為Exit，動作是關閉程式。
            
            self.edit=self.menuBar().addMenu("&Edit")  #功能表新增Edit，單純測試用
            self.edit.addAction('&Delete',self.close)
            self.edit.addAction('&Copy',self.close)
    
        def _createToolBar(self):
            tools = QToolBar()
            self.addToolBar(tools)
            tools.addAction('Exit', self.close)
            tools.addAction('Escape', self.close)
    
        def _createStatusBar(self):
            status = QStatusBar()
            status.showMessage("I'm the Status Bar")
            self.setStatusBar(status)
    
    if __name__ == '__main__':
        app = QApplication(sys.argv)
        win = Window()
        win.setGeometry(200, 200, 280, 280)
        win.show()
        sys.exit(app.exec())
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/

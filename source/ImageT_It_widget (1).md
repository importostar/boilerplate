---
title: ImageT_It_widget (1)
date: 2020-05-07
---
Example Python program ImageT_It_widget (1).py
This program creates a PyQt GUI

## Modules

* import sys
* from PyQt5.QtWidgets import (QMainWindow,QAction, qApp, QToolTip, QWidget,
* from  PyQt5.QtGui import QIcon, QFont
* from PyQt5.QtCore import QCoreApplication

## Classes

* class Widgetmain(QMainWindow):

## Methods

* def __init__(self):
* def initUI(self):
* def center(self):
* def closeEvent(self, event):

## Code

Example Python PyQt program :

    # -*- coding: utf-8 -*-
    """
    Pyqt5 Image Tool demo
    """
    import sys
    from PyQt5.QtWidgets import (QMainWindow,QAction, qApp, QToolTip, QWidget,
        QPushButton, QApplication,QMessageBox, QDesktopWidget,QHBoxLayout, QVBoxLayout )
    from  PyQt5.QtGui import QIcon, QFont
    from PyQt5.QtCore import QCoreApplication
    
    class Widgetmain(QMainWindow):
    
        def __init__(self):
            super().__init__()
            self.initUI()
    
        def initUI(self):
            #菜单
            exitAction = QAction(QIcon('quit.png'), '&Exit', self)
            exitAction.setShortcut('Ctrl+Q')
            exitAction.setStatusTip('Exit application')
    
            exitAction.triggered.connect(qApp.quit)
    
            menubar = self.menuBar()
            fileMenu = menubar.addMenu('&File')
            fileMenu.addAction(exitAction)
    
            self.toolbar = self.addToolBar('Exit!')
            self.toolbar.addAction(exitAction)
    
            # QToolTip.setFont(QFont('SansSerif', 10))
            # self.setToolTip('This is a <b>QWidget</b> widget')
    
            # btn = QPushButton('Button', self)
            # btn.setToolTip('This is a <b>QPushButton</b> widget')
            # btn.resize(btn.sizeHint())
            # btn.move(50, 50)
            #
            # qbtn = QPushButton('Quit', self)
            # qbtn.clicked.connect(QCoreApplication.instance().quit)
            # qbtn.resize(btn.sizeHint())
            # qbtn.move(150, 50)
    
            #按钮安装
            okbutton = QPushButton("OK")
            cancelButton = QPushButton("Cancel")
            hbox = QHBoxLayout()
            hbox.addStretch(1)
            hbox.addWidget(okbutton)
            hbox.addWidget(cancelButton)
    
            vbox = QVBoxLayout()
            vbox.addStretch(1)
            vbox.addLayout(hbox)
    
            self.setLayout(vbox)
    
            #标题、logo、界面大小
            # self.resize(800,400)
            self.setGeometry(300, 300, 800, 400)
            self.setWindowTitle('Image Tool')
            self.setWindowIcon(QIcon('cbp.ico'))
    
            self.center()
            self.statusBar().showMessage('Ready')
            self.show()
    
        def center(self):
            qr = self.frameGeometry()
            cp = QDesktopWidget().availableGeometry().center()
            qr.moveCenter(cp)
            self.move(qr.topLeft())
    
        def closeEvent(self, event):
    
            reply = QMessageBox.question(self,'Message',"Are you sure to quit", QMessageBox.Yes |
                QMessageBox.No, QMessageBox.No )
    
            if reply == QMessageBox.Yes:
                event.accept()
            else:
                event.ignore()
    
    
    if __name__ == '__main__':
    
        app = QApplication(sys.argv)
        ex = Widgetmain()
        # w = QWidget()
        # w.resize(800, 600)
        # w.move(800, 300)
        # w.setWindowTitle('Image Tools Demo')
        # w.show()
    
        sys.exit(app.exec_())
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/

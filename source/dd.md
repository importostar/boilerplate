---
title: dd
date: 2020-05-07
---
Example Python program dd.py
This program creates a PyQt GUI
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import sys
* from PyQt5.QtWidgets import QWidget, QDesktopWidget, QApplication, QMainWindow, QFrame, QTableView, QVBoxLayout, QAbstractItemView
* from PyQt5 import QtGui, QtCore

## Classes

* class MyTableView(QTableView):
* class MyModel(QtGui.QStandardItemModel):
* class Example(QMainWindow):

## Methods

* def dropEvent(self, e):
* #def dropMimeData(self, data, action, row, column, parent):
* def supportedDragActions(self):
* def canDropMimeData(self, *args):
* #def dropMimeData(self, data, action, row, column, parent):
* def __init__(self):
* def center(self):

## Code

Example Python PyQt program :

    #!/usr/bin/python3
    # -*- coding: utf-8 -*-
    
    import sys
    from PyQt5.QtWidgets import QWidget, QDesktopWidget, QApplication, QMainWindow, QFrame, QTableView, QVBoxLayout, QAbstractItemView
    from PyQt5 import QtGui, QtCore
    
    
    class MyTableView(QTableView):
        # Model with activated DragDrop functionality
        # vor view
        def dropEvent(self, e):
            #print(dir(e))
            #print (e.mimeData())
            pos = e.pos()
            row = self.rowAt(pos.y())
            index = self.model().index(row,0)
            print(index.data())
            #print(index)
    
            for url in e.mimeData().urls():
                #path = url.toLocalFile().toLocal8Bit().data()
                print(url)
    
                #if os.path.isfile(path):
                #    print(path)
    
    
    
        #def dropMimeData(self, data, action, row, column, parent):
        #    print('\n{}\n{}\n{}\n{}\n{}'.format(data, action, row, column, parent))
        #    return True
    
    class MyModel(QtGui.QStandardItemModel):
        # Model with activated DragDrop functionality
        # vor view
        def supportedDragActions(self):
            #print("asks supported drop actions")
            return Qt.LinkAction | Qt.CopyAction
    
        def canDropMimeData(self, *args):
            #print("canDropMimeData")
            return True
    
        #def dropMimeData(self, data, action, row, column, parent):
        #    print('\n{}\n{}\n{}\n{}\n{}'.format(data, action, row, column, parent))
        #    return True
    
    
    
    class Example(QMainWindow):
        
        def __init__(self):
            super().__init__()
            
            #self.resize(300, 400)
            #self.center()
            self.setGeometry(200, 200, 300, 400)
            
            
            main_frame = QFrame()
            self.setCentralWidget(main_frame)
            vbox = QVBoxLayout(main_frame)
    
            #self.tableview = QTableView()
            self.tableview = MyTableView()
            self.tableview.setDropIndicatorShown(True)
            self.tableview.setDragEnabled(True)
            self.tableview.setAcceptDrops(True)
            self.tableview.setDragDropMode(QTableView.DragDrop)
            self.tableview.setDefaultDropAction(QtCore.Qt.LinkAction)
            self.tableview.setDropIndicatorShown(True)
    
            #self.tableview.setDropIndicatorShown(True)
            #self.tableview.setAcceptDrops(True)
            #self.tableview.setDragEnabled(True)
            #self.tableview.setDragDropMode(QAbstractItemView.InternalMove )
    
            #filter = Filter(self)
            #self.tableview.installEventFilter(filter)
    
            vbox.addWidget(self.tableview)
    
            #self.model = QtGui.QStandardItemModel()
            self.model = MyModel()
            self.tableview.setModel(self.model)
    
            item = QtGui.QStandardItem('Test')
            item.setFlags(QtCore.Qt.ItemIsEnabled | QtCore.Qt.ItemIsSelectable | QtCore.Qt.ItemIsDragEnabled | QtCore.Qt.ItemIsDropEnabled)
            self.model.appendRow(item)
    
            item = QtGui.QStandardItem('Test 2')
            item.setFlags(QtCore.Qt.ItemIsEnabled | QtCore.Qt.ItemIsSelectable | QtCore.Qt.ItemIsDragEnabled | QtCore.Qt.ItemIsDropEnabled)
            self.model.appendRow(item)
    
            self.setWindowTitle('Center')    
            self.show()
            
            
        def center(self):
            
            qr = self.frameGeometry()
            cp = QDesktopWidget().availableGeometry().center()
            qr.moveCenter(cp)
            self.move(qr.topLeft())
            
            
    if __name__ == '__main__':
        
        app = QApplication(sys.argv)
        ex = Example()
        sys.exit(app.exec_()) 

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/

---
title: listview
date: 2020-05-07
---
Example Python program listview.py
This program creates a PyQt GUI
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* from PyQt5 import QtCore, QtGui, QtWidgets, uic
* from PyQt5.QtCore import Qt
* import sys

## Classes

* class EmptyModel(QtCore.QStringListModel):
* class StringListModel(QtCore.QStringListModel):
* class SelectableModel(EmptyModel):

## Methods

* def __init__(self, n):
* def rowCount(self, parent):
* def data(self, index, role):
* def __init__(self, data):
* def rowCount(self, parent):
* def data(self, index, role):
* def __init__(self, n):
* def select(self, index):

## Code

Example Python PyQt program :

    from PyQt5 import QtCore, QtGui, QtWidgets, uic
    from PyQt5.QtCore import Qt
    
    
    COLORS = [QtGui.QColor(n) for n in ['pink', 'skyblue', 'red']]
    
    
    class EmptyModel(QtCore.QStringListModel):
        '''データの個数だけを記録し、要素の値はインデックスから計算する。'''
    
        def __init__(self, n):
            super().__init__()
            self.n = n
    
        def rowCount(self, parent):
            return self.n
    
        def data(self, index, role):
            i = index.row()
            if role == Qt.DisplayRole:      return i * i
            elif role == Qt.BackgroundRole: return COLORS[i % 2]
    
    
    class StringListModel(QtCore.QStringListModel):
        '''self.data にデータを保存する。'''
    
        def __init__(self, data):
            super().__init__()
            self.data = data
    
        def rowCount(self, parent):
            return len(self.data)
    
        def data(self, index, role):
            i = index.row()
            if role == Qt.DisplayRole:      return self.data[i]
            elif role == Qt.BackgroundRole: return COLORS[i % 2]
    
    
    class SelectableModel(EmptyModel):
        '''クリックされたデータを表示する'''
    
        def __init__(self, n):
            super().__init__(n)
    
        def select(self, index):
            print('{1}@{0}'.format(index.row(), self.data(index, Qt.DisplayRole)))
    
    
    if __name__ == '__main__':
        import sys
    
        app = QtWidgets.QApplication(sys.argv)
    
        models = [EmptyModel(100),
                  StringListModel([str(i * i) for i in range(100)]),
                  SelectableModel(100)]
    
        for model in models:
            view = QtWidgets.QListView()
            view.setModel(model)
            view.setWindowTitle(model.__class__.__doc__)
            if model == models[2]:
                view.clicked.connect(view.model().select)
            view.show()
            app.exec()
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/

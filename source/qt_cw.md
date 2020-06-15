---
title: qt_cw
date: 2020-05-07
---
Example Python program qt_cw.py

## Modules

* from PyQt5 import QtCore
* from PyQt5.QtCore import Qt, pyqtSignal, QPoint
* from PyQt5.QtWidgets import (QWidget, QLineEdit, QHBoxLayout)

## Classes

* class MyLineEdit(QLineEdit):
* class QSymbolSearch(QWidget):

## Methods

* def __init__(self, parent):
* def _clearBtnClicked(self):
* def focusInEvent(self, event):
* def focusOutEvent(self, event):
* def keyPressEvent(self, e):
* def __init__(self, parent):
* def keyPressHandler(self, e=None):
* def cancelHandler(self, e=None):
* def focusInHandler(self):
* def focusOutHandler(self):

## Code

Example Python PyQt program :

    from PyQt5 import QtCore
    from PyQt5.QtCore import Qt, pyqtSignal, QPoint
    from PyQt5.QtWidgets import (QWidget, QLineEdit, QHBoxLayout)
    
    class MyLineEdit(QLineEdit):
        focusIn = pyqtSignal()
        focusOut = pyqtSignal()
        enterPressed = pyqtSignal(str)
        cancelPressed = pyqtSignal()
        clearBtnClicked = pyqtSignal()
    
        def __init__(self, parent):
           super().__init__(parent)
    
        def _clearBtnClicked(self):
            self.clearBtnClicked.emit()
    
        def focusInEvent(self, event):
            self.focusIn.emit()
            super().focusInEvent(event)
    
        def focusOutEvent(self, event):
            self.focusOut.emit()
            super().focusOutEvent(event)
    
        def keyPressEvent(self, e):
            if e.key() in [Qt.Key_Enter, Qt.Key_Return]:
                self.enterPressed.emit(self.text())
            if e.key() in [Qt.Key_Escape]:
                self.cancelPressed.emit()
            super().keyPressEvent(e)
    
    
    class QSymbolSearch(QWidget):
        enterPressed = pyqtSignal(str)
        cancelSearch = pyqtSignal()
        
        def __init__(self, parent):
            super().__init__(parent)
            #self.setFocusPolicy(Qt.StrongFocus)
            lay = QHBoxLayout(self)
            lay.setContentsMargins(0, 0, 0, 0)
            self.input = MyLineEdit(self)
            self.input.focusIn.connect(self.focusInHandler)
            self.input.focusOut.connect(self.focusOutHandler)
            self.input.enterPressed.connect(self.keyPressHandler)
            self.input.cancelPressed.connect(self.cancelHandler)
            lay.addWidget(self.input)  
    
        def keyPressHandler(self, e=None):
            if e == None or not isinstance(e, str): 
                e = self.input.text()
     
            self.enterPressed.emit(e)
    
        def cancelHandler(self, e=None):
            self.cancelSearch.emit()
    
        def focusInHandler(self):
            pass
    
        def focusOutHandler(self):
            pass
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/

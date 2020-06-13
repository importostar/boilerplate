---
title: QClipboard
date: 2020-05-07
---
Example Python program QClipboard.py
This program creates a PyQt GUI

## Modules

* import sys
* from PyQt5 import QtWidgets
* from PyQt5 import QtGui
* from PyQt5.QtCore import pyqtSlot # pyqtSlot 프로퍼티를 사용하기 위함

## Classes

* class Form(QtWidgets.QDialog):

## Methods

* def __init__(self, parent=None):
* def slot_copy_clipboard_1(self):
* def slot_copy_clipboard_2(self):

## Code

Example Python PyQt program :

    # coding: utf-8
    
    import sys
    from PyQt5 import QtWidgets
    from PyQt5 import QtGui
    from PyQt5.QtCore import pyqtSlot # pyqtSlot 프로퍼티를 사용하기 위함
    
    datas = ['정철아','문서를','보면','다 나온다']
    
    
    class Form(QtWidgets.QDialog):
        def __init__(self, parent=None):
            QtWidgets.QDialog.__init__(self, parent)
            self.setGeometry(100,100,250,100)
    
            self.cb = QtWidgets.QComboBox(self)
            self.cb.addItems(datas)
            self.bt_1 = QtWidgets.QPushButton('복사', self)
            self.bt_1.clicked.connect(self.slot_copy_clipboard_1)
            hbox_1 = QtWidgets.QHBoxLayout()
            hbox_1.addWidget(self.cb)
            hbox_1.addWidget(self.bt_1)
    
            self.le = QtWidgets.QLineEdit(self)
            self.bt_2 = QtWidgets.QPushButton('복사', self)
            self.bt_2.clicked.connect(self.slot_copy_clipboard_2)
            hbox_2 = QtWidgets.QHBoxLayout()
            hbox_2.addWidget(self.le)
            hbox_2.addWidget(self.bt_2)
    
            self.te = QtWidgets.QTextEdit(self)
    
            vbox = QtWidgets.QVBoxLayout()
            vbox.addLayout(hbox_1)
            vbox.addLayout(hbox_2)
            vbox.addWidget(self.te)
    
            self.setLayout(vbox)
    
            self.qclip = QtWidgets.QApplication.clipboard()
    
    
        @pyqtSlot()
        def slot_copy_clipboard_1(self):
            self.qclip.setText(self.cb.currentText())
    
        @pyqtSlot()
        def slot_copy_clipboard_2(self):
            self.qclip.setText(self.le.text())
    
    if __name__ == '__main__':
        app = QtWidgets.QApplication(sys.argv)
        w = Form()
        w.show()
        sys.exit(app.exec())
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/

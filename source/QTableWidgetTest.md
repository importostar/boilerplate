---
title: QTableWidgetTest
date: 2020-05-07
---
Example Python program QTableWidgetTest.py
This program creates a PyQt GUI

## Modules

* from PyQt5.QtGui import * 
* from PyQt5.QtCore import * 
* from PyQt5.QtWidgets import * 
* import sys

## Classes

* class Widget(QWidget):

## Methods

* def __init__(self, parent=None):
* def onClicked(self):
* def main():  

## Code

Example Python PyQt program :

    from PyQt5.QtGui import * 
    from PyQt5.QtCore import * 
    from PyQt5.QtWidgets import * 
    import sys
    
    class Widget(QWidget):
        def __init__(self, parent=None):
            QWidget.__init__(self, parent)
            self.setLayout(QVBoxLayout())
            self.le =  QLineEdit(":P", self)
            self.le.setPlaceholderText("Value to be changed")
            self.combo = QComboBox(self)
            btn =  QPushButton("Press Me to Change", self)
            btn.clicked.connect(self.onClicked)
            self.table = QTableWidget(self)
    
            self.layout().addWidget(self.le)
            self.layout().addWidget(self.combo)
            self.layout().addWidget(btn)
            self.layout().addWidget(self.table)
    
            self.table.setRowCount(4)
            self.table.setColumnCount(2)
    
            for i in range(self.table.rowCount()):
                for j in range(self.table.columnCount()):
                    self.table.setItem(i, j, QTableWidgetItem("Item ({},{})".format(i, j)))
    
            self.combo.addItems(["{}, {}".format(i, j) for i in range(self.table.rowCount()) for j in range(self.table.columnCount())])
    
        def onClicked(self):
            x, y =  self.combo.currentText().split(",")
            self.table.item(int(x), int(y)).setText(self.le.text())
    
    def main():  
        app 	= QApplication(sys.argv)
    
        widget =  Widget()
        widget.show()
        return app.exec_()
     
    if __name__ == '__main__':
        main()

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/

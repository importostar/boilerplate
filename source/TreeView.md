---
title: TreeView
date: 2020-05-07
---
Example Python program TreeView.py
This program creates a PyQt GUI

## Modules

* from PyQt5.QtCore import *
* from PyQt5.QtGui  import *
* from PyQt5.QtWidgets import *
* import sys

## Classes

* class MyMainWindow(QMainWindow):
* class FormWidget(QWidget):

## Methods

* def __init__(self, parent=None):
* def __init__(self, parent):

## Code

Example Python PyQt program :

    from PyQt5.QtCore import *
    from PyQt5.QtGui  import *
    from PyQt5.QtWidgets import *
    
    
    
    import sys
    
    
    
    class MyMainWindow(QMainWindow):
    
        def __init__(self, parent=None):
    
            super(MyMainWindow, self).__init__(parent)
            self.form_widget = FormWidget(self)
            self.setCentralWidget(self.form_widget)
    
    
    
    class FormWidget(QWidget):
    
        def __init__(self, parent):
            super(FormWidget, self).__init__(parent)
            self.layout = QVBoxLayout(self)
            self.view = QTreeView()
            self.view.setSelectionBehavior(QAbstractItemView.SelectRows)
    
            model = QStandardItemModel()
    
            model.setHorizontalHeaderLabels(['col1', 'col2', 'col3'])
    
            self.view.setModel(model)
    
            self.view.setUniformRowHeights(True)
    
        # ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    
        # populate data
    
            for i in range(3):
    
                parent1 = QStandardItem('Family {}. Some long status text for sp'.format(i))
    
                for j in range(3):
    
                    child1 = QStandardItem('Child {}'.format(i*3+j))
    
                    child2 = QStandardItem('row: {}, col: {}'.format(i, j+1))
    
                    child3 = QStandardItem('row: {}, col: {}'.format(i, j+2))
    
                    parent1.appendRow([child1, child2, child3])
    
                model.appendRow(parent1) #if this line in second for loop, there's a duplicate insertion warning
    
            # span container columns
            #Display whole message of first collumm of each element
                self.view.setFirstColumnSpanned(i, self.view.rootIndex(), True)
    
        # ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    
        # expand third container
    
            index = model.indexFromItem(parent1)
    
            self.view.expand(index)
    
        # ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    
        # select last row
    
            selmod = self.view.selectionModel()
    
            index2 = model.indexFromItem(child3)
    
            selmod.select(index2, QItemSelectionModel.Select|QItemSelectionModel.Rows)
            self.layout.addWidget(self.view)
            self.button1 = QPushButton("Button 1")
            self.layout.addWidget(self.button1)
    
            self.button2 = QPushButton("Button 2")
            self.layout.addWidget(self.button2)
    
    #text edit widget
            self.text = QLineEdit()
            self.layout.addWidget(self.text)
    
    # checklist widget
            self.salutations = ['Ahoy',
                                'Good day',
                                'Hello',
                                'Heyo',
                                'Hi',
                                'Salutations',
                                'Wassup',
                                'Yo']
            self.salutation = QComboBox()
            self.salutation.addItems(self.salutations)
            self.salutation.setMinimumWidth(285)
            self.salutation.move(110, 5)
    
            self.layout.addWidget(self.salutation)
            self.setLayout(self.layout)
    
    app = QApplication([])
    foo = MyMainWindow()
    foo.show()
    sys.exit(app.exec_())
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/

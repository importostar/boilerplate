---
title: sorting_qtableview
date: 2020-05-07
---
Example Python program sorting_qtableview.py
This program creates a PyQt GUI

## Modules

* import sys
* from PyQt5.QtCore import (Qt,
* from PyQt5.QtWidgets import (QApplication,

## Classes

* class SortingTableModel(QAbstractTableModel):

## Methods

* def __init__(self, parent=None):
* def headerData(self, section, orientation, role):
* def data(self, index, role):
* def columnCount(self, parent):
* def rowCount(self, parent):
* def insertRows(self, position, rows, parent=QModelIndex()):

## Code

Example Python PyQt program :

    # Applying a sort feature in a QTableView
    
    import sys
    from PyQt5.QtCore import (Qt,
                              QModelIndex,
                              QAbstractTableModel,
                              QSortFilterProxyModel)
    from PyQt5.QtWidgets import (QApplication,
                                 QTableView)
    
    HEADER = ['Qty', 'Fruit']
    DATA = [[10, 'Starfruit'],
            [12, 'Orange'],
            [54, 'Kiwi'],
            [7, 'Bapples']]
    
    
    # Creating the table model
    class SortingTableModel(QAbstractTableModel):
    
        def __init__(self, parent=None):
    
            super().__init__(parent)
    
        def headerData(self, section, orientation, role):
    
            if role == Qt.DisplayRole:
                if orientation == Qt.Horizontal:
                    return HEADER[section]
    
        def data(self, index, role):
    
            row = index.row()
            col = index.column()
    
            if role == Qt.DisplayRole:
                value = DATA[row][col]
                return value
    
        def columnCount(self, parent):
    
            return len(HEADER)
    
        def rowCount(self, parent):
    
            return len(DATA)
    
        def insertRows(self, position, rows, parent=QModelIndex()):
    
            self.beginInsertRows(parent, position, position + rows - 1)
            self.endInsertRows()
            return True
    
    
    if __name__ == '__main__':
        app = QApplication(sys.argv)
    
        # How to apply sorting in a QTableView
    
        # Step 1: create the model for the QTableView
        tablemodel = SortingTableModel()
        tablemodel.insertRows(len(DATA), 1)
    
        # Step 2: create the sorter model
        sortermodel = QSortFilterProxyModel()
        sortermodel.setSourceModel(tablemodel)
        sortermodel.setFilterKeyColumn(3)
    
        # Step 3: setup the QTableView to enable sorting
        tableview = QTableView()
        tableview.setWindowTitle('Sorting QTableView')
        tableview.setModel(sortermodel)
        tableview.setSortingEnabled(True)
        tableview.sortByColumn(1, Qt.AscendingOrder)   # sorting via 'Fruit' header
        tableview.show()
    
        sys.exit(app.exec())
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/

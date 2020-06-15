---
title: orderconversion (1)
date: 2020-05-07
---
Example Python program orderconversion (1).py

## Modules

* from PyQt5.QtWidgets import QHeaderView, QTableWidgetItem
* from PyQt5.QtCore import Qt
* from ui_orderconversion import Ui_OrderConversion

## Classes

* class OrderConversion(Ui_OrderConversion):

## Methods

* def __init__(self, *args, **kwargs):
* def add_row(self):
* def column_width(self):

## Code

Example Python PyQt program :

    from PyQt5.QtWidgets import QHeaderView, QTableWidgetItem
    from PyQt5.QtCore import Qt
    from ui_orderconversion import Ui_OrderConversion
    
    class OrderConversion(Ui_OrderConversion):
    
        def __init__(self, *args, **kwargs):
            super().__init__(*args, **kwargs)
            # initialize ui
            self.setupUi(self)
            #set column width by running column_width()
            self.column_width()
    
            # create checkbox item, set state to unchecked, add to row 0 column 1,4
            checkbox = QTableWidgetItem()
            checkbox.setCheckState(Qt.Unchecked)
            self.orders_table.setItem(0, 1, checkbox)
            self.orders_table.setItem(0, 4, checkbox)
    
            # if cell is changed run method add_row
            self.orders_table.cellChanged.connect(self.add_row)
    
            # dispaly ui
            self.show()
    
        def add_row(self):
            '''Add row if order number added to first cell in each column'''
            # add needed data to variables
            rc = self.orders_table.rowCount()
            c_row = self.orders_table.currentRow()
            c_col = self.orders_table.currentColumn()
            value = self.orders_table.item(c_row, c_col)
            value = value.text()
    
            # create checkbox item and set state to unchecked
            checkbox = QTableWidgetItem()
            checkbox.setCheckState(Qt.Unchecked)
    
            # insert row and checkbox if condition is met
            if c_col == 0 and len(value) == 2:
                self.orders_table.insertRow(rc)
                self.orders_table.setItem(c_row, 1, checkbox)
    
        def column_width(self):
            '''Adds headers to each column and sets wdith'''
            col_headers = ['OrderNum', 'Converted/Printed', 'FaxEmail', 'RequestDate', 'HOT']
            self.orders_table.setHorizontalHeaderLabels(col_headers)
            self.orders_table.horizontalHeader().setStretchLastSection(True)
            self.orders_table.setColumnWidth(1, 120)
            self.orders_table.horizontalHeader().setSectionResizeMode(0, QHeaderView.Stretch)

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/

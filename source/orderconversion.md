---
title: orderconversion
date: 2020-05-07
---
Example Python program orderconversion.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* from PyQt5.QtWidgets import QHeaderView
* from ui_orderconversion import Ui_OrderConversion

## Classes

* class OrderConversion(Ui_OrderConversion):

## Methods

* def __init__(self):
* def add_row(self):
* def column_width(self):
* def column_checkbox(self):

## Code

Example Python PyQt program :

    from PyQt5.QtWidgets import QHeaderView
    from ui_orderconversion import Ui_OrderConversion
    
    class OrderConversion(Ui_OrderConversion):
    
        def __init__(self):
            super().__init__()
            self.setupUi(self)
            self.column_width()
    
            self.orders_table.cellChanged.connect(self.add_row)
    
            self.show()
    
        def add_row(self):
            '''Add row if order number added to first cell in each column'''
            c_row = self.orders_table.currentRow()
            c_col = self.orders_table.currentColumn()
            value = self.orders_table.item(c_row, c_col)
            value = value.text()
            rc = self.orders_table.rowCount()
            if c_col == 0 and len(value) == 2:
                self.orders_table.insertRow(rc)
    
        def column_width(self):
            '''Adds headers to each column and sets wdith'''
            col_headers = ['OrderNum', 'Converted/Printed', 'FaxEmail', 'RequestDate', 'HOT']
            self.orders_table.setHorizontalHeaderLabels(col_headers)
            self.orders_table.horizontalHeader().setStretchLastSection(True)
            self.orders_table.setColumnWidth(1, 120)
            self.orders_table.horizontalHeader().setSectionResizeMode(0, QHeaderView.Stretch)
    
        def column_checkbox(self):
            '''Add checkbox to column 1 and 4'''
            '''Currently just print statements, will change soon'''
            #print(self.orders_table.columnCount())
            #print(self.orders_table.rowCount())
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/

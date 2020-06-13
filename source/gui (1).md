---
title: gui (1)
date: 2020-05-07
---
Example Python program gui (1).py
This program creates a PyQt GUI

## Modules

* from PyQt5.QtWidgets import QMainWindow, QApplication
* from PyQt5.QtCore import pyqtSignal
* from MainWindow import Ui_MainWindow
* import sys
* from converter import convert, DEFAULT_TABLE

## Classes

* class MainWindow(QMainWindow, Ui_MainWindow):

## Methods

* def __init__(self, number: str = None, original_base: int = 10, result_base: int = 10, table: str = None):
* def compute(self, from_number: bool):
* def start(number: str = None, original_base: int = 10, result_base: int = 10, table: str = None):

## Code

Example Python PyQt program :

    #!/usr/bin/env python3
    # -*- coding: utf-8 -*-
    
    from PyQt5.QtWidgets import QMainWindow, QApplication
    from PyQt5.QtCore import pyqtSignal
    from MainWindow import Ui_MainWindow
    import sys
    from converter import convert, DEFAULT_TABLE
    
    
    class MainWindow(QMainWindow, Ui_MainWindow):
        number_changed = pyqtSignal(str, name='numberChanged')
        result_changed = pyqtSignal(str, name='resultChanged')
    
        def __init__(self, number: str = None, original_base: int = 10, result_base: int = 10, table: str = None):
            super().__init__(None)
            self.setupUi(self)
    
            self.computing = False
    
            self.number_changed['QString'].connect(self.resultNumberLineEdit.setText)
            self.result_changed['QString'].connect(self.originalNumberLineEdit.setText)
            self.originalNumberLineEdit.textEdited.connect(lambda: self.compute(True))
            self.resultNumberLineEdit.textEdited.connect(lambda: self.compute(False))
    
            self.originalBaseLineEdit.setText(str(original_base))
            self.resultBaseLineEdit.setText(str(result_base))
            if table and table != DEFAULT_TABLE:
                self.usingTableCheckBox.setChecked(True)
                self.tableLabel.setEnabled(True)
                self.tableLineEdit.setEnabled(True)
                self.tableLineEdit.setText(table)
            if number:
                self.originalNumberLineEdit.setText(number)
                self.compute(True)
    
        def compute(self, from_number: bool):
            if from_number:
                number = self.originalNumberLineEdit.text()
                original_base = self.originalBaseLineEdit.text()
                result_base = self.resultBaseLineEdit.text()
            else:
                number = self.resultNumberLineEdit.text()
                original_base = self.resultBaseLineEdit.text()
                result_base = self.originalBaseLineEdit.text()
            table = self.tableLineEdit.text() if self.usingTableCheckBox.isChecked() else DEFAULT_TABLE
    
            try:
                result = convert(number, original_base, result_base, table)
            except (ValueError, IndexError):
                result = ''
            if from_number:
                self.number_changed[str].emit(result)
            else:
                self.result_changed[str].emit(result)
    
    
    def start(number: str = None, original_base: int = 10, result_base: int = 10, table: str = None):
        application = QApplication([])
        main_window = MainWindow(number, original_base, result_base, table)
        main_window.show()
        sys.exit(application.exec())
    
    
    if __name__ == '__main__':
        start()
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/

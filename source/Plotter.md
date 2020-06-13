---
title: Plotter
date: 2020-05-07
---
Example Python program Plotter.py
This program creates a PyQt GUI
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import pandas as pd
* from PyQt5.QtCore import QRegularExpression, pyqtSignal
* from PyQt5.QtGui import QIcon, QRegularExpressionValidator, QValidator
* from PyQt5.QtWidgets import QTableWidget, QApplication, QTableWidgetItem, QMenu, QInputDialog, QLineEdit, QMainWindow, \
* import sys

## Classes

* class SelectionWidget(QWidget):
* class CompareDialog(QDialog):
* class MainWindow(QMainWindow):
* class TableLabel(QWidget):
* class Table(QTableWidget):
* class NameDialog(QDialog):

## Methods

* def __init__(self, items, parent=None):
* def getRows(self):
* def check_state(self, text):
* def __init__(self, names, parent=None):
* def onCliked(self):
* def addSelections(self):
* def __init__(self, parent=None):
* def loadFile(self):
* def onCompare(self):
* def createPlot(self, config):
* def __init__(self, filename, text, parent=None):
* def __init__(self, fileName, name, parent=None):
* def rowbyIndex(self, row):
* def contextMenuEvent(self, event):
* def __init__(self, names, parent=None):
* def check_state(self, text):

## Code

Example Python PyQt program :

    #!/usr/bin/env python
    # -*- coding: utf-8 -*-
    
    import pandas as pd
    from PyQt5.QtCore import QRegularExpression, pyqtSignal
    from PyQt5.QtGui import QIcon, QRegularExpressionValidator, QValidator
    from PyQt5.QtWidgets import QTableWidget, QApplication, QTableWidgetItem, QMenu, QInputDialog, QLineEdit, QMainWindow, \
        QDialog, QVBoxLayout, QLabel, QHBoxLayout, QComboBox, QToolButton, QPushButton, QSpacerItem, QSizePolicy, \
        QWidget, QFileDialog, QDialogButtonBox
    
    
    class SelectionWidget(QWidget):
        completed = pyqtSignal(bool)
    
        def __init__(self, items, parent=None):
            QWidget.__init__(self, parent)
            self.setLayout(QHBoxLayout())
            self.combobox = QComboBox(self)
            self.combobox.addItems(items)
            self.layout().addWidget(self.combobox)
            self.le = QLineEdit(self)
            self.le.setValidator(QRegularExpressionValidator(QRegularExpression("^([0-9])+(,[0-9]+)*$"), self))
            self.le.textChanged.connect(self.check_state)
            self.layout().addWidget(self.le)
            btnDelete = QToolButton(self)
            btnDelete.setIcon(QIcon.fromTheme("edit-delete"))
            self.layout().addWidget(btnDelete)
            btnDelete.clicked.connect(self.deleteLater)
    
        def getRows(self):
            return self.combobox.currentText(), [int(el) for el in self.le.text().split(",")]
    
        def check_state(self, text):
            sender = self.sender()
            validator = sender.validator()
            state = validator.validate(text, 0)[0]
            if state == QValidator.Acceptable:
                color = '#c4df9b'  # green
                self.completed.emit(True)
            elif state == QValidator.Intermediate:
                color = '#fff79a'  # yellow
                self.completed.emit(False)
            else:
                color = '#f6989d'  # red
                self.completed.emit(True)
            sender.setStyleSheet('QLineEdit { background-color: %s }' % color)
    
    
    class CompareDialog(QDialog):
        def __init__(self, names, parent=None):
            QDialog.__init__(self, parent)
            self.setLayout(QVBoxLayout())
            self.setWindowTitle("Perspective - MultiGraph Window")
            self.names = names
            self.selectWidgetList = []
            self.config = {}
    
            ly = QHBoxLayout()
            ly.addWidget(QLabel("Input Format Table Name row, numbers, seperated, with, commas", self))
    
            addBtn = QPushButton("Add", self)
            addBtn.clicked.connect(self.addSelections)
            addBtn.setAutoDefault(False)
            ly.addWidget(addBtn)
            self.layout().addLayout(ly)
    
            self.selectionsLayout = QVBoxLayout()
            self.layout().addLayout(self.selectionsLayout)
    
            hlayout = QHBoxLayout()
            hlayout.addItem(QSpacerItem(0, 10, QSizePolicy.Expanding, QSizePolicy.MinimumExpanding))
    
            self.boxPlot = QPushButton("Box Plot", self)
            self.scatterPlot = QPushButton("Scatter Plot", self)
            self.boxPlot.setEnabled(False)
            self.scatterPlot.setEnabled(False)
            self.boxPlot.clicked.connect(self.onCliked)
            self.scatterPlot.clicked.connect(self.onCliked)
            hlayout.addWidget(self.boxPlot)
            hlayout.addWidget(self.scatterPlot)
    
            self.addSelections()
    
            self.layout().addLayout(hlayout)
    
        def onCliked(self):
            if self.sender() == self.boxPlot:
                self.config['type'] = 'box'
            else:
                self.config['type'] = 'scatter'
            selected = []
    
            for w in self.selectWidgetList:
                selected.append(w.getRows())
            self.config['values'] = selected
            self.accept()
    
        def addSelections(self):
            w = SelectionWidget(self.names, self)
            w.completed.connect(self.boxPlot.setEnabled)
            w.completed.connect(self.scatterPlot.setEnabled)
            self.selectWidgetList.append(w)
            self.selectionsLayout.addWidget(w)
    
    
    class MainWindow(QMainWindow):
        def __init__(self, parent=None):
            QMainWindow.__init__(self, parent)
            self.setCentralWidget(QWidget(self))
            self.centralWidget().setLayout(QVBoxLayout())
    
            self.tableDicts = {}
    
            hbox = QHBoxLayout()
            hbox.addWidget(QLineEdit())
    
            loadFileBtn = QPushButton("Load File")
            loadFileBtn.clicked.connect(self.loadFile)
    
            compareBtn = QPushButton("Compare")
            compareBtn.clicked.connect(self.onCompare)
    
            hbox.addWidget(loadFileBtn)
            hbox.addWidget(compareBtn)
    
            self.centralWidget().layout().addLayout(hbox)
            self.tbLayout = QVBoxLayout()
            self.centralWidget().layout().addLayout(self.tbLayout)
    
        def loadFile(self):
            fileName, _ = QFileDialog.getOpenFileName(self, "QFileDialog.getOpenFileName()", "",
                                                      "(*.csv)")
    
            if fileName != "":
                dial = NameDialog(self.tableDicts.keys(), self)
                if dial.exec_() == QDialog.Accepted and dial.text != "":
                    tl = TableLabel(fileName, dial.text, self)
                    self.tableDicts[dial.text] = tl
                    self.tbLayout.addWidget(tl)
    
        def onCompare(self):
            dial = CompareDialog(self.tableDicts.keys())
            if dial.exec_() == QDialog.Accepted:
                self.createPlot(dial.config)
    
        def createPlot(self, config):
            values = config['values']
            type_plot = config['type']
            for name, rows in values:
                tb = self.tableDicts[name].tb
                for row in rows:
                    if row < tb.rowCount():
                        l = tb.rowbyIndex(row)
                        print(type_plot, name, row,  l)
    
    
    class TableLabel(QWidget):
        def __init__(self, filename, text, parent=None):
            QWidget.__init__(self, parent)
            self.tb = Table(filename, text, self)
            self.setLayout(QVBoxLayout())
            self.layout().addWidget(QLabel(text, self))
            self.layout().addWidget(self.tb)
            self.tb.destroyed.connect(self.deleteLater)
    
    
    class Table(QTableWidget):
        def __init__(self, fileName, name, parent=None):
            QTableWidget.__init__(self, parent)
            data = pd.read_csv(fileName, encoding="ISO-8859-1")
            self.name = name
    
            drop_names = ['Nominal Value', 'median', 'Tolerance', 'mean', 'min', 'max', 'range', 'Deviation', 'variance', 'Standard Deviation', 'LowerBound', 'UpperBound', 'Unnamed: 0']
    
            for drop_name in drop_names:
            	data.drop(drop_name, axis=1, inplace=True)
    
            headers = data.columns.values
    
            self.setColumnCount(len(headers))
            self.setRowCount(len(data.index))
            self.setHorizontalHeaderLabels(headers)
    
            for i in range(self.rowCount()):
                for j in range(self.columnCount()):
                    item = QTableWidgetItem(str(round(data.ix[i, j], 5)))
                    self.setItem(i, j, item)
    
        def rowbyIndex(self, row):
            if row < self.rowCount():
                return [float(self.item(row, j).text()) for j in range(self.columnCount())]
    
        def contextMenuEvent(self, event):
            menu = QMenu(self)
            graphAction = menu.addAction("Graph")  # Boxplt
    
            scatterAction = menu.addAction("Scatter Plot")
            checkAttributesAction = menu.addAction("Table Attributes")
    
            ReNameAction = menu.addAction("Rename")
            printNameAction = menu.addAction("Name?")
            printAction = menu.addAction("Print Row")
            quitAction = menu.addAction("Close Table")
    
            action = menu.exec_(self.mapToGlobal(event.pos()))
    
            if action == quitAction:
                self.deleteLater()
            elif action == ReNameAction:
                text, ok = QInputDialog.getText(self, "Table Properties", "Enter Table Name", QLineEdit.Normal, self.name)
                if ok and text != "":
                    self.name = text
            elif action == printNameAction:
                print(self.name)
    
    
    class NameDialog(QDialog):
        def __init__(self, names, parent=None):
            QDialog.__init__(self, parent)
            self.setWindowTitle("Table Name")
            self.names = names
            self.setLayout(QVBoxLayout())
            self.layout().addWidget(QLabel("Enter table name"))
            le = QLineEdit(self)
            le.textChanged.connect(self.check_state)
            self.layout().addWidget(le)
            self.suggestionsLb = QLabel(self)
            self.suggestionsLb.hide()
            self.suggestionsLb.setStyleSheet("background-color: #f6989d")
            self.layout().addWidget(self.suggestionsLb)
            self.buttonBox = QDialogButtonBox(QDialogButtonBox.Ok | QDialogButtonBox.Cancel)
            self.buttonBox.accepted.connect(self.accept)
            self.buttonBox.rejected.connect(self.reject)
            self.buttonBox.button(QDialogButtonBox.Ok).setEnabled(False)
            self.layout().addWidget(self.buttonBox)
    
            self.text = ""
    
        def check_state(self, text):
            if text in self.names:
                self.suggestionsLb.setText("The Name has already been assigned.")
                self.suggestionsLb.show()
                self.buttonBox.button(QDialogButtonBox.Ok).setEnabled(False)
            elif text == "":
                self.buttonBox.button(QDialogButtonBox.Ok).setEnabled(False)
            else:
                self.buttonBox.button(QDialogButtonBox.Ok).setEnabled(True)
                self.suggestionsLb.hide()
                self.text = text
    
    
    if __name__ == '__main__':
        import sys
    
        app = QApplication(sys.argv)
        w = MainWindow()
        w.show()
        sys.exit(app.exec_())
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/

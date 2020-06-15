---
title: load (1)
date: 2020-05-07
---
Example Python program load (1).py
This program creates a PyQt GUI
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import sys
* import time
* from PyQt5.QtWidgets import *
* from PyQt5.QtGui import *
* from PyQt5.QtCore import *
* from table import Ui_MainWindow

## Classes

* class main(QMainWindow):
* class threadTable(QThread):

## Methods

* def __init__(self):
* def add_row(self,counter):
* def table(self):
* def __init__(self, parent=None):
* def run(self):

## Code

Example Python PyQt program :

    import sys
    import time
    from PyQt5.QtWidgets import *
    from PyQt5.QtGui import *
    from PyQt5.QtCore import *
    from table import Ui_MainWindow
    
    class main(QMainWindow):
        def __init__(self):
            super(main, self).__init__()
            self.ui = Ui_MainWindow()
            self.ui.setupUi(self)
            self.table()
            self.myThread = threadTable()
            self.myThread.updated.connect(self.add_row)
            self.myThread.start()
    
    
        pyqtSlot(int)
        def add_row(self,counter):
            try:
                i = counter
            except ValueError:
                print("Error!")
            else:            
    
                rowPosition = self.ui.tableWidget.rowCount()
                self.ui.tableWidget.insertRow(rowPosition)
            
                item1 = QTableWidgetItem("item" + str(i))
                item2 = QTableWidgetItem("item" + str(i))
                item3 = QTableWidgetItem("item" + str(i))
                item4 = QTableWidgetItem("item" + str(i))
                item5 = QTableWidgetItem("item" + str(i))
    
                item1.setTextAlignment(Qt.AlignHCenter | Qt.AlignVCenter | Qt.AlignCenter)
                item2.setTextAlignment(Qt.AlignHCenter | Qt.AlignVCenter | Qt.AlignCenter)
                item3.setTextAlignment(Qt.AlignHCenter | Qt.AlignVCenter | Qt.AlignCenter)
                item4.setTextAlignment(Qt.AlignHCenter | Qt.AlignVCenter | Qt.AlignCenter)
                item5.setTextAlignment(Qt.AlignHCenter | Qt.AlignVCenter | Qt.AlignCenter)
    
                self.ui.tableWidget.setItem(rowPosition, 0, QTableWidgetItem(item1))  # item1
                self.ui.tableWidget.setItem(rowPosition, 1, QTableWidgetItem(item2))  # item2
                self.ui.tableWidget.setItem(rowPosition, 2, QTableWidgetItem(item3))  # item3
                self.ui.tableWidget.setItem(rowPosition, 3, QTableWidgetItem(item4))  # item4
                self.ui.tableWidget.setItem(rowPosition, 4, QTableWidgetItem(item5))  # item5   
    
    
    
        def table(self):
            # Deshabilitar edición
            self.ui.tableWidget.setEditTriggers(QAbstractItemView.NoEditTriggers)
            # Deshabilitar el comportamiento de arrastrar y soltar
            self.ui.tableWidget.setDragDropOverwriteMode(False)
            # Seleccionar toda la fila
            self.ui.tableWidget.setSelectionBehavior(QAbstractItemView.SelectRows)
            # Establecer el número de columnas
            self.ui.tableWidget.setColumnCount(5)
            # Establecer el número de filas
            self.ui.tableWidget.setRowCount(0)
            # Alineación del texto del encabezado
            self.ui.tableWidget.horizontalHeader().setDefaultAlignment(Qt.AlignHCenter | Qt.AlignVCenter | Qt.AlignCenter)
            # Ocultar encabezado vertical
            self.ui.tableWidget.verticalHeader().setVisible(False)
            nombreColumnas = ('header1', 'header2', 'header3', 'header4', 'header5')
            # Establecer las etiquetas de encabezado horizontal usando etiquetas
            self.ui.tableWidget.setHorizontalHeaderLabels(nombreColumnas)
            # todo los headers de la tabla se ponen del mismo tamaño
            self.ui.tableWidget.horizontalHeader().setSectionResizeMode(QHeaderView.Stretch)
    
    class threadTable(QThread):
        updated = pyqtSignal(int)
        def __init__(self, parent=None):
            super(threadTable, self).__init__(parent)
            self.done = False
    
        def run(self):
            counter = 0
            for i in range(100000):
                counter += 1
                time.sleep(0.1)
                self.updated.emit(counter)
    
    
    if __name__ == '__main__':
        app = QApplication([])
        application = main()
        application.show()
        sys.exit(app.exec())

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/

---
title: RFIDRegister_Main
date: 2020-05-07
---
Example Python program RFIDRegister_Main.py
This program creates a PyQt GUI

## Modules

* from datetime import datetime
* import sys
* from PyQt5 import QtSql, QtCore
* from PyQt5.QtCore import QDateTime
* from PyQt5.QtSql import QSqlQuery
* from PyQt5.QtWidgets import QMainWindow, QApplication, QMessageBox
* from WindowUI import Ui_MainWindow

## Classes

* class MainWindow(QMainWindow, Ui_MainWindow):

## Methods

* def __init__(self, *args, **kwargs):
* def get_events(self):
* def go_back(self):
* def insert_row(self):
* def delete_row(self):
* def before_exit(self):
* def main():

## Code

Example Python PyQt program :

    from datetime import datetime
    import sys
    
    from PyQt5 import QtSql, QtCore
    from PyQt5.QtCore import QDateTime
    from PyQt5.QtSql import QSqlQuery
    from PyQt5.QtWidgets import QMainWindow, QApplication, QMessageBox
    
    from WindowUI import Ui_MainWindow
    
    
    class MainWindow(QMainWindow, Ui_MainWindow):
    
        def __init__(self, *args, **kwargs):
            super(MainWindow, self).__init__(*args, **kwargs)
            self.setupUi(self)
            self.onEvents = False
            self.db = QtSql.QSqlDatabase.addDatabase('QPSQL')
            self.db.setHostName("localhost")
            self.db.setDatabaseName("rfid_register")
            self.db.setUserName("postgres")
            self.db.setPassword("postgres")
            self.db.setPort(5432)
            ok = self.db.open()
            if not ok:
                QMessageBox.warning(self, 'Error!', "Error connecting to database.")
                sys.exit()
            self.tableModel = QtSql.QSqlTableModel(self, self.db)
            self.tableModel.setTable("markers")
            self.tableView.setModel(self.tableModel)
            self.tableModel.select()
            self.getEvents.clicked.connect(self.get_events)
            self.goBack.clicked.connect(self.go_back)
            self.goBack.setVisible(False)
            self.insertButton.clicked.connect(self.insert_row)
            self.deleteButton.clicked.connect(self.delete_row)
    
        def get_events(self):
            query = QSqlQuery(self.db)
            query.prepare("SELECT * FROM markers WHERE rfid_id = :rfid_id")
            query.bindValue(":rfid_id", self.rfidIDField.text().strip(" "))
            query.exec()
            found = query.next()
            if not found:
                QMessageBox.warning(self, 'Error!', "No marker with rfid_id "
                                    + self.rfidIDField.text().strip(" ") + " found.")
                return
            self.tableModel.setTable("events")
            self.tableModel.setFilter("rfid_id = '" + self.rfidIDField.text().strip(" ") + "'")
            self.tableModel.select()
            self.goBack.setVisible(True)
            self.getEvents.setVisible(False)
            self.label.setVisible(False)
            self.label_2.setText(self.rfidIDField.text().strip(" "))
            self.label_2.setVisible(True)
            self.rfidIDField.setText("")
            self.rfidIDField.setVisible(False)
            self.onEvents = True
    
        def go_back(self):
            self.tableModel.setTable("markers")
            self.tableModel.select()
            self.goBack.setVisible(False)
            self.getEvents.setVisible(True)
            self.rfidIDField.setVisible(True)
            self.label_2.setVisible(False)
            self.label.setVisible(True)
            self.onEvents = False
    
        def insert_row(self):
            record = QtSql.QSqlRecord()
            record.append(QtSql.QSqlField('id', QtCore.QVariant.Int))
            record.append(QtSql.QSqlField('rfid_id', QtCore.QVariant.String))
            record.append(QtSql.QSqlField('description', QtCore.QVariant.String))
            record.setValue('id', 0)
            if self.onEvents:
                record.append(QtSql.QSqlField('date', QtCore.QVariant.DateTime))
                record.setValue('date', QDateTime.currentDateTime())
                record.setValue('rfid_id', self.label_2.text())
            else:
                if self.rfidIDField.text().strip(" ") == "":
                    QMessageBox.warning(self, 'Error!', "Need to fill ID of marker field to insert new marker.")
                    return
                query = QSqlQuery(self.db)
                query.prepare("SELECT * FROM markers WHERE rfid_id = :rfid_id")
                query.bindValue(":rfid_id", self.rfidIDField.text().strip(" "))
                query.exec()
                found = query.next()
                if found:
                    QMessageBox.warning(self, 'Error!', "Marker with such id already exists.")
                    return
                record.setValue('rfid_id', self.rfidIDField.text().strip(" "))
            self.tableModel.insertRecord(-1, record)
            self.tableModel.select()
    
        def delete_row(self):
            index = self.tableView.currentIndex()
            self.tableModel.removeRows(index.row(), 1)
            self.tableModel.select()
    
        def before_exit(self):
            self.db.close()
    
    
    def main():
        app = QApplication(sys.argv)
        GUI = MainWindow()
        app.aboutToQuit.connect(GUI.before_exit)
        GUI.show()
        sys.exit(app.exec_())
    
    
    main()

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/

---
title: Employe
date: 2020-05-07
---
Example Python program Employe.py
This program creates a PyQt GUI
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* from PyQt5.QtWidgets import *
* from PyQt5.QtGui import QPixmap, QFont
* import sys
* import os
* import sqlite3
* from sqlite3 import Error

## Classes

* class Main(QWidget):
* class EmployeeDB:

## Methods

* def __init__(self):
* def UI(self):
* def main_desing(self):
* def layouts(self):
* def __init__(self, db_filename):
* def Create_connection(self, db_filename):
* def Crear_table(self, conn, query):
* def main():

## Code

Example Python PyQt program :

    # -*- coding: utf8 -*-
    # Programa: employee.py
    # Objetivo: Desarrollar un CRUD con PyQt5
    # Autor: Christian Mejia
    # Fecha: 16/marzo/2020
    
    from PyQt5.QtWidgets import *
    from PyQt5.QtGui import QPixmap, QFont
    import sys
    import os
    import sqlite3
    from sqlite3 import Error
    
    employee_id = None
    
    
    class Main(QWidget):
        """ Ventana principal de la Aplicación. """
    
        def __init__(self):
            super().__init__()
            self.setWindowTitle("CRUD de empleados")
            self.setGeometry(450, 150, 750, 600)
            self.UI()
            self.show()
            # Crear o abrir la coneccion a la bd
            self.employee_db = EmployeeDB("employee.db")
    
        def UI(self):
            """ Definimos los objetos que componen la interfaz de usuario. """
            self.main_desing()
            self.layouts()
    
        def main_desing(self):
            """ Diseño principal de la aplicación. """
            self.employee_list = QListWidget()
            self.btn_new = QPushButton("Agregar")
            self.btn_update = QPushButton("Modificar")
            self.btn_delete = QPushButton("Eliminar")
    
        def layouts(self):
            """ Layouts que componen la aplicación. """
            # Layouts
            self.main_layout = QHBoxLayout()
            self.left_layout = QFormLayout()
            self.right_main_layout = QVBoxLayout()
            self.right_top_layout = QHBoxLayout()
            self.right_bottom_layout = QHBoxLayout()
    
            # Agregar los layouts hijos al layout padre
            self.right_main_layout.addLayout(self.right_top_layout)
            self.right_main_layout.addLayout(self.right_bottom_layout)
            self.main_layout.addLayout(self.left_layout, 40)
            self.main_layout.addLayout(self.right_main_layout, 60)
    
            # Agregar widgets a los layouts
            self.right_top_layout.addWidget(self.employee_list)
            self.right_bottom_layout.addWidget(self.btn_new)
            self.right_bottom_layout.addWidget(self.btn_update)
            self.right_bottom_layout.addWidget(self.btn_delete)
    
            # Colocar el layout principal en la ventana principal
            self.setLayout(self.main_layout)
    
    class EmployeeDB:
    
        def __init__(self, db_filename):
            """ Inicializador de la clase """
            self.Create_connection(db_filename)
            self.employee_query = """ Create table if not exist employe(
                                        id integer PRIMARY KEY,
                                        nombre text NOT NULL,
                                        identidad text NOT NULL,
                                        telefono text NOT NULL,
                                        email text NOT NULL,
                                        direccion text,
                                        imagen text
                                        );
                                        """
    
            self.Crear_table(self.Create_connection,self.employee_query)
    
        """ Base de datos SQLite para los empleados. """
        def Create_connection(self, db_filename):
            """ Crear una conexxion a la base de datos SQLite """
            conn = None
    
            try:
                conn = sqlite3.connect(db_filename)
                print("Conexion realizada. Version {0}".format( sqlite3.version))
            except Error as e:
                print(e)
            finally:
                return conn
    
        def Crear_table(self, conn, query):
            """ 
            Crea una tabla basado en los valores del query. 
            :param conn: Conexion con la BD
            :param query: La instruccion Create Table
            :return:
            """
            try:
                cursor = conn.cursor()
                cursor.execute(query)
            except Error as e:
                print(e)
    
    
    
    def main():
        app = QApplication(sys.argv)
        window = Main()
        sys.exit(app.exec_())
    
    
    if __name__ == "__main__":
        main()

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/

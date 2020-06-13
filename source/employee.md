---
title: employee
date: 2020-05-07
---
Example Python program employee.py
This program creates a PyQt GUI
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import sys
* import os
* import sqlite3
* from sqlite3 import Error
* from PyQt5.QtWidgets import *
* from PyQt5.QtGui import QPixmap, QFont
* from PIL import Image

## Classes

* class Main(QWidget):
* class EmployeeDB:
* class AddEmployee(QWidget):

## Methods

* def __init__(self):
* def UI(self):
* def main_desing(self):
* def layouts(self):
* def add_employee(self):
* def set_employee_list(self):
* def show_employee(self):
* def delete_employee(self):
* def __init__(self, db_filename):
* def create_connection(self, db_filename):
* def create_table(self, conn, query):
* def add_employee(self, employee):
* def get_all_employee(self):
* def get_employee_by_id(self, id):
* def delete_employee_by_id(self, id):
* def __init__(self, employee_db):
* def UI(self):
* def mainDesing(self):
* def layouts(self):
* def upload_image(self):
* def insert(self):
* def main():

## Code

Example Python PyQt program :

    # -*- coding: utf8 -*-
    # Programa: employee.py
    # Objetivo: Desarrollar un CRUD con PyQt5
    # Autor: Héctor Sabillón
    # Fecha: 16/marzo/2020
    
    import sys
    import os
    import sqlite3
    from sqlite3 import Error
    from PyQt5.QtWidgets import *
    from PyQt5.QtGui import QPixmap, QFont
    from PIL import Image
    
    employee_id = None
    
    
    class Main(QWidget):
        """ Ventana principal de la Aplicación. """
    
        def __init__(self):
            super().__init__()
            # Crear o abrir la conexión a la base de datos
            self.employee_db = EmployeeDB("employee.db")
            self.setWindowTitle("CRUD de empleados")
            self.setGeometry(450, 150, 750, 600)
            self.UI()
            self.show()
    
        def UI(self):
            """ Definimos los objetos que componen la interfaz de usuario. """
            self.main_desing()
            self.layouts()
            self.set_employee_list()
    
        def main_desing(self):
            """ Diseño principal de la aplicación. """
            self.employee_list = QListWidget()
            self.employee_list.itemClicked.connect(self.show_employee)
            self.btn_new = QPushButton("Agregar")
            self.btn_new.clicked.connect(self.add_employee)
            self.btn_update = QPushButton("Modificar")
            self.btn_delete = QPushButton("Eliminar")
            self.btn_delete.clicked.connect(self.delete_employee)
    
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
    
        def add_employee(self):
            """ Inicia el formulario de ingreso de datos del empleado """
            self.new_employee = AddEmployee(self.employee_db)
            self.close()
    
        def set_employee_list(self):
            """ Obtiene las tuplas de empleados y las muestra en la lista """
            employees = self.employee_db.get_all_employee()
    
            if employees:
                for employee in employees:
                    self.employee_list.addItem(
                        "{0} --- {1}".format(employee[1], employee[2]))
    
        def show_employee(self):
            """ Muestra los atributos del empleado que se encuentra seleccionado """
            # Remover los widgets que se encuentran en self.left_layout
            for x in reversed(range(self.left_layout.count())):
                # Remover los widgets uno por uno
                widget = self.left_layout.takeAt(x).widget()
    
                if widget is not None:
                    widget.deleteLater()
    
            # Obtener el valor de la identidad del empleado seleccionado
            employee = self.employee_list.currentItem().text()
            id = employee.split(" --- ")[0]
    
            employee = self.employee_db.get_employee_by_id(id)
    
            # Crear y agregar los widget necesarios para mostrar la información
            if employee:
                image = QLabel()
                image.setPixmap(QPixmap("images/{employee[6]"))
                card_number = QLabel(employee[1])
                name = QLabel(employee[2])
                telephone = QLabel(employee[3])
                email = QLabel(employee[4])
                address = QLabel(employee[5])
    
                self.left_layout.addRow("", image)
                self.left_layout.addRow("Identidad:", card_number)
                self.left_layout.addRow("Nombre:", name)
                self.left_layout.addRow("Teléfono:", telephone)
                self.left_layout.addRow("Correo electrónico:", email)
                self.left_layout.addRow("Dirección:", address)
    
        def delete_employee(self):
            """ Elimina el empleado que se encuentra seleccionado """
            # Obtener el valor de la identidad del empleado seleccionado
            # Verificar que un elemento de la lista se encuentre seleccionado
            if self.employee_list.selectedItems():
                employee = self.employee_list.currentItem().text()
                id = employee.split(" --- ")[0]
    
                employee = self.employee_db.get_employee_by_id(id)
    
                yes = QMessageBox.Yes
    
                if employee:
                    question_text = f"¿Está seguro de eliminar el empleado {employee[1]}?"
                    question = QMessageBox.question(self, "Advertencia", question_text,
                        QMessageBox.Yes | QMessageBox.No, QMessageBox.No)
    
                    if question == QMessageBox.Yes:
                        self.employee_db.delete_employee_by_id(employee[1])
                        QMessageBox.information(self, "Información", "¡Empleado eliminado satisfactoriamente!")
    
                else:
                    QMessageBox.information(self, "Advertencia", "Ha ocurrido un error. Reintente nuevamente")
    
            else:
                QMessageBox.information(self, "Advertencia", "Favor seleccionar un empleado a eliminar")
    
    
    class EmployeeDB:
        """ Base de datos SQLite para los empleados. """
    
        def __init__(self, db_filename):
            """ Inicializador de la clase """
            self.connection = self.create_connection(db_filename)
            self.employee_query = """ CREATE TABLE IF NOT EXISTS employee (
                                        id integer PRIMARY KEY,
                                        identidad text NOT NULL,
                                        nombre text NOT NULL,
                                        telefono text NOT NULL,
                                        email text NOT NULL,
                                        direccion text,
                                        imagen text
                                      );
                                    """
            self.create_table(self.connection, self.employee_query)
    
        def create_connection(self, db_filename):
            """ Crear una conexión a la base de datos SQLite """
            conn = None
    
            # Tratar de conectarse con SQLite y crear la base de datos
            try:
                conn = sqlite3.connect(db_filename)
                print("Conexión realizada. Versión {}".format(sqlite3.version))
            except Error as e:
                print(e)
            finally:
                return conn
    
        def create_table(self, conn, query):
            """
            Crea una tabla basado en los valores de query.
            :param conn: Conexión con la base de datos.
            :param query: La instrucción CREATE TABLE.
            :return:
            """
            try:
                cursor = conn.cursor()
                cursor.execute(query)
            except Error as e:
                print(e)
    
        def add_employee(self, employee):
            """
            Realiza una inserción a la tabla de empleados.
            :param employee: Una estructura que contiene
                             los datos del empleado.
            :return:
            """
            sqlInsert = """
                        INSERT INTO employee(
                            identidad, nombre, telefono,
                            email, direccion, imagen)
                         VALUES(?, ?, ?, ?, ?, ?)
                        """
    
            try:
                cursor = self.connection.cursor()
                cursor.execute(sqlInsert, employee)
                # Indicarle al motor de base de datos
                # que los cambios sean persistentes
                self.connection.commit()
            except Error as e:
                print(e)
    
        def get_all_employee(self):
            """ Obtiene todas las tuplas de la tabla employee """
            sqlQuery = " SELECT * FROM employee ORDER BY ROWID ASC "
    
            try:
                cursor = self.connection.cursor()
                employees = cursor.execute(sqlQuery).fetchall()
    
                return employees
            except Error as e:
                print(e)
    
            return None
    
        def get_employee_by_id(self, id):
            """
            Busca un empleado mediante el valor de la identidad.
    
            param: id: El valor de la tarjeta de identidad del empleado.
            :return: Un arreglo con los atributos del empleado.
            """
            sqlQuery = " SELECT * FROM employee WHERE identidad = ?"
    
            try:
                cursor = self.connection.cursor()
                # fetchone espera que se retorne una tupla (1,)
                employee = cursor.execute(sqlQuery, (id,)).fetchone()
    
                return employee
            except Error as e:
                print(e)
    
            return None
    
        def delete_employee_by_id(self, id):
            """
            Elimina un empleado mediante el valor de la identidad.
    
            param: id: El valor de la tarjeta de identidad del empleado.
            :return: True si el empleado se eliminó. None en caso contrario.
            """
            sqlQuery = " DELETE FROM employee WHERE identidad = ? "
    
            try:
                cursor = self.connection.cursor()
                cursor.execute(sqlQuery, (id,))
                self.connection.commit()
    
                return True
            except Error as e:
                print(e)
    
            return None
    
    
    class AddEmployee(QWidget):
        """ Muestra la ventana para agregar nuevos empleados. """
    
        def __init__(self, employee_db):
            super().__init__()
            # Conexión a la base de datos
            self.employee_db = employee_db
            self.setWindowTitle("Agregar un empleado")
            self.setGeometry(450, 150, 750, 600)
            self.UI()
            self.show()
    
        def UI(self):
            """ Cargar los layouts de diseño de la ventana """
            self.mainDesing()
            self.layouts()
    
        def mainDesing(self):
            """ Crear los widgets que conforman la interfaz """
            # Top Layout Widgets
            self.title = QLabel("Agregar empleado")
            self.image = QLabel()
            self.image.setPixmap(QPixmap("images/agregar-usuario.png"))
    
            # Bottom Layout Widgets
            self.label_id = QLabel("Identidad: ")
            self.input_id = QLineEdit()
            self.input_id.setPlaceholderText("0318-2000-01234")
            self.label_name = QLabel("Nombre completo: ")
            self.input_name = QLineEdit()
            self.input_name.setPlaceholderText("Jon Snow")
            self.label_phone = QLabel("Teléfono: ")
            self.input_phone = QLineEdit()
            self.input_phone.setPlaceholderText("9999-0000")
            self.label_email = QLabel("Correo electrónico: ")
            self.input_email = QLineEdit()
            self.input_email.setPlaceholderText("jon.snow@winterfell.com")
            self.label_address = QLabel("Dirección: ")
            self.textedit_address = QTextEdit()
            self.label_image = QLabel("Fotografía: ")
            self.button_image = QPushButton("Buscar")
            self.button_image.clicked.connect(self.upload_image)
            self.button_add = QPushButton("Agregar")
            self.button_add.clicked.connect(self.insert)
    
        def layouts(self):
            """ Define la estructura de los elementos en pantalla """
            # Main layouts
            self.main_layout = QVBoxLayout()
            self.top_layout = QVBoxLayout()
            self.bottom_layout = QFormLayout()
    
            # Agregar los widgets (childrens) al main_layout
            self.main_layout.addLayout(self.top_layout)
            self.main_layout.addLayout(self.bottom_layout)
    
            # Agregar los widgets al top layout
            self.top_layout.addWidget(self.title)
            self.top_layout.addWidget(self.image)
    
            # Agregar los widgets al bottom layout
            self.bottom_layout.addRow(self.label_id, self.input_id)
            self.bottom_layout.addRow(self.label_name, self.input_name)
            self.bottom_layout.addRow(self.label_phone, self.input_phone)
            self.bottom_layout.addRow(self.label_email, self.input_email)
            self.bottom_layout.addRow(self.label_address, self.textedit_address)
            self.bottom_layout.addRow(self.label_image, self.button_image)
            self.bottom_layout.addRow("", self.button_add)
    
            # Establecer el layout principal de la ventana
            self.setLayout(self.main_layout)
    
        def upload_image(self):
            """ Permite subir una imagen de perfil del empleado """
            size = (256, 256)
            self.filename, ok = QFileDialog.getOpenFileName(
                self, "Agregar foto perfil", "", "Imágenes (*.jpg *.png)")
    
            # Si el usuario acepta el cuadro de diálogo seleccionando
            # una imagen.
            if ok:
                self.fullpath = os.path.basename(self.filename)
                # Implementar PIL (Python Imaging Library) para abrir
                # la imagen, cambiarle el tamaño y almacenarla.
                image = Image.open(self.filename)
                image = image.resize(size)
                image.save(f"images/{self.fullpath}")
    
        def insert(self):
            """ Insertar los valores del formulario a la tabla de empleado """
            # Verificar si los valores requeridos fueron agregados
            if (self.input_id.text() or self.input_name.text() or
                    self.input_phone.text() or self.input_email.text() != ""):
                employee = (self.input_id.text(), self.input_name.text(),
                            self.input_phone.text(), self.input_email.text(),
                            self.textedit_address.toPlainText(), "")
    
                try:
                    self.employee_db.add_employee(employee)
                    QMessageBox.information(
                        self, "Información", "Empleado agregado correctamente")
                    self.close()
                    self.main = Main()
                except Error as e:
                    QMessageBox.information(
                        self, "Error", "Error al momento de agregar el empleado")
            else:
                QMessageBox.information(
                    self, "Advertencia", "Debes ingresar toda la información")
    
    
    def main():
        app = QApplication(sys.argv)
        window = Main()
        sys.exit(app.exec_())
    
    
    if __name__ == "__main__":
        main()

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/

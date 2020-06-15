---
title: qt5example
date: 2020-05-07
---
Example Python program qt5example.py
This program creates a PyQt GUI
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import os
* import sys
* from PyQt5.QtWidgets import QMainWindow, QAction, qApp, QApplication, QFileDialog
* from PyQt5.QtGui import QIcon
* from PyQt5 import QtCore, QtWidgets
* # Estas dos líneas son las importantes:

## Classes

* class ToolBarVertical(QMainWindow):

## Methods

* def __init__(self):
* def _abrir_filefialog(self, *args):

## Code

Example Python PyQt program :

    #!/usr/bin/python
    # -*- coding: utf-8 -*-
    
    import os
    import sys
    
    from PyQt5.QtWidgets import QMainWindow, QAction, qApp, QApplication, QFileDialog
    from PyQt5.QtGui import QIcon
    from PyQt5 import QtCore, QtWidgets
    
    
    class ToolBarVertical(QMainWindow):
    
        def __init__(self):
            QMainWindow.__init__(self)
    
            acciones = [
                ("Abrir", "document-open", "Ctrl+O", self._abrir_filefialog),
                ("Guardar", "document-save", "Ctrl+S", None),
                ("Salir", "exit", "Ctrl+Q", qApp.exit),
            ]
    
            # Estas dos líneas son las importantes:
            self.toolbar = QtWidgets.QToolBar()
            self.addToolBar(QtCore.Qt.LeftToolBarArea, self.toolbar)
    
            for accion in acciones:
                nombre, icono, shortcut, callback= accion
    
                qaction = QAction(QIcon.fromTheme(icono), nombre, self)
    
                if shortcut is not None:
                    qaction.setShortcut("Ctrl+Q")
    
                if callback is not None:
                    qaction.triggered.connect(callback)
    
                self.toolbar.addAction(qaction)
    
            self.setGeometry(400, 200, 620, 480)
            self.setWindowTitle("ToolBar Vertical")
            self.show()
    
        def _abrir_filefialog(self, *args):
            # Le digo que no use el nativo solo porque el de plasma es horrible,
            # si lo dejás normal a vos te va a salir el de Gtk de toda la vida.
            opciones = QFileDialog.Options() | QFileDialog.DontUseNativeDialog
    
            # Defino qué extensiones son permitidas dentro de un filtro.
            lenguajes =\
                "*.py "\
                "*.sh " +\
                "*.vala " +\
                "*.js " +\
                "*.html " +\
                "*.php " +\
                "*.h " +\
                "*.cpp" +\
                "*.pas" +\
                "*.java" +\
                "*.css" +\
                "*.go"
    
            # Otro filto para cualquier tipo de archivo, por si acaso.
            todos = "*"
    
            archivos, filtros = QFileDialog.getOpenFileNames(
                self, # Ventana
                "Abrir archivo", # Título
                os.path.expanduser("~/"), # Directorio al abrir
                "Archivos de código (%s);;Todos los ficheros (*)" % lenguajes, # Filtros
                options=opciones) # Otras configuraciones del FileDialog
    
            print("Archivos seleccionados: ", archivos)  # archivos es una lista, si el usuario cancela va a estar vacía
    
    
    if __name__ == "__main__":
        app = QApplication(sys.argv)
        ex = ToolBarVertical()
        sys.exit(app.exec_())
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/

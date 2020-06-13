---
title: gui2
date: 2020-05-07
---
Example Python program gui2.py
This program creates a PyQt GUI
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import sys
* from PyQt5.QtWidgets import (QWidget, QGridLayout,

## Methods

* def deleteClickEvent():

## Code

Example Python PyQt program :

    # http://zetcode.com/gui/pyqt5/ - iesaku iziet cauri shim tutorialim
    
    import sys
    from PyQt5.QtWidgets import (QWidget, QGridLayout,
                                 QPushButton, QApplication, QLabel, QMessageBox)
    
    
    #PyQT obligati nepieciesams izveidot QApplication objektu
    app = QApplication([])
    
    # Viss parejais var tikt veidots procedurali, bet labaak izmantot OOP pieeju, kas aprakstita tutoriali un kuru Tu jau biji meginajis
    
    w = QWidget()
    grid = QGridLayout()
    w.setLayout(grid)
    grid.setSpacing(10)
    
    # Buttons
    list_all_cars_btn = QPushButton("Show me the cars")
    add_car_btn = QPushButton("Add car")
    edit_car_btn = QPushButton("Edit car")
    delete_car_btn = QPushButton("Delete a car")
    quit_btn = QPushButton("Quit")
    
    # Lets create some button action
    # 1 - quit
    quit_btn.clicked.connect(QApplication.instance().quit)
    
    # 2 - delete
    def deleteClickEvent():
        reply = QMessageBox.question(w, 'Message',
                                     "Vai tiesam dzesam?", QMessageBox.Yes |
                                     QMessageBox.No, QMessageBox.No)
        if reply == QMessageBox.Yes:
            print('Do some delete stuff') # print to console
            info_label_q.setText("Car has been deleted")
    
    delete_car_btn.clicked.connect(deleteClickEvent)
    
    # List of labels
    list_all_cars_q = QLabel('Press this button to view all your cars')
    add_car_q = QLabel('Add a car to your database')
    edit_car_q = QLabel("Edit a car's record")
    delete_car_q = QLabel('Delete a car from database')
    info_label_q = QLabel('Try to press Delete button...')
    
    # POSITIONS
    grid.addWidget(list_all_cars_q, 1, 0)
    grid.addWidget(list_all_cars_btn, 1, 1)
    grid.addWidget(add_car_q, 2, 0)
    grid.addWidget(add_car_btn, 2, 1)
    grid.addWidget(edit_car_q, 3, 0)
    grid.addWidget(edit_car_btn, 3, 1)
    grid.addWidget(delete_car_q, 4, 0)
    grid.addWidget(delete_car_btn, 4, 1)
    grid.addWidget(info_label_q, 5,0)
    grid.addWidget(quit_btn, 6, 2)
    
    w.setLayout(grid)
    w.setGeometry(300, 300, 350, 300)
    w.setWindowTitle('Main menu - Vehicle manager')
    w.show()
    
    sys.exit(app.exec_())
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/

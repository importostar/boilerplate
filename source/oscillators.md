---
title: oscillators
date: 2020-05-07
---
Example Python program oscillators.py
This program creates a PyQt GUI
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import sys
* from PyQt5.QtCore import pyqtSignal
* from PyQt5.QtWidgets import QMainWindow, QApplication, QPushButton, QWidget, QGridLayout, QCheckBox

## Classes

* class MainWindow(QMainWindow):
* class ChoiceWidget(QWidget):
* class OpenGLWidget(QWidget):

## Methods

* def __init__(self):
* def main_window_init(self):
* def switch_widgets(self):
* def __init__(self, parent):
* def widget_init(self):
* def start_oscillators(self):
* def __init__(self, parent):
* def widget_init(self):
* def on_start_signal(self, argument):

## Code

Example Python PyQt program :

    import sys
    
    from PyQt5.QtCore import pyqtSignal
    from PyQt5.QtWidgets import QMainWindow, QApplication, QPushButton, QWidget, QGridLayout, QCheckBox
    
    class MainWindow(QMainWindow):
        # fenetre principale, elle contient tout les trucs que tu vois s'afficher
        def __init__(self):
            super().__init__()
    
            # initialisation des widgets que la fenêtre contient
            self.main_widget = ChoiceWidget(parent=self)
            self.openGL_widget = OpenGLWidget(parent=self)
    
            self.main_window_init()
    
        def main_window_init(self):
            # Signals
    
            # tu utilises cette classe pour relier les deux widgets entre eux
            self.main_widget.send_oscillators_to_start_signal.connect(self.openGL_widget.receive_oscillator_to_start_signal)
    
            # et pour changer le widget qui s'affiche
            self.main_widget.switch_widgets_signal.connect(self.switch_widgets)
    
    
            self.setCentralWidget(self.main_widget)
            #                 x    y  x_size y_size
            self.setGeometry(300, 300, 300, 200)
            self.setWindowTitle('OOOOOOOOscillateurs')
            self.show()
    
        def switch_widgets(self):
            self.setCentralWidget(self.openGL_widget)
    
    
    class ChoiceWidget(QWidget):
        switch_widgets_signal = pyqtSignal()
        send_oscillators_to_start_signal = pyqtSignal([dict])
    
        def __init__(self, parent):
            # this allow the use of the parent's methods when needed
            super(ChoiceWidget, self).__init__(parent=parent)
    
            self.oscillator_1 = QCheckBox("Oscillateur 1")
            self.oscillator_2 = QCheckBox("Oscillateur 2")
            self.oscillator_3 = QCheckBox("Oscillateur 3")
    
            self.start_button = QPushButton("Start !")
            self.widget_init()
    
        def widget_init(self):
            """
            Ca c'est super pratique: ça fait une grille et tu places les widgets dedans. Imagine un echequier dont l'index
            commence en haut à gauche
            """
            grid = QGridLayout()
            self.setLayout(grid)
    
            self.start_button.clicked.connect(self.start_oscillators)
    
            #                     pos_verticale, pos horizontale
            grid.addWidget(self.oscillator_1, 0, 0)
            grid.addWidget(self.oscillator_2, 1, 0)
            grid.addWidget(self.oscillator_3, 2, 0)
            grid.addWidget(self.start_button, 1, 2)
    
        def start_oscillators(self):
            # isChecked retourne true si la case est cochée
            a = {1: self.oscillator_1.isChecked(), 2: self.oscillator_2.isChecked(), 3: self.oscillator_3.isChecked()}
            self.send_oscillators_to_start_signal.emit(a)
            self.switch_widgets_signal.emit()
    
    class OpenGLWidget(QWidget):
        receive_oscillator_to_start_signal = pyqtSignal([dict])
    
        def __init__(self, parent):
            # this allow the use of the parent's methods when needed
            super().__init__(parent=parent)
            self.widget_init()
    
        def widget_init(self):
            # lorsqu'un signal est emit, Qt appelle la fonction avec comme paramètre le dictionaire qui est transmit par le signal
            self.receive_oscillator_to_start_signal.connect(self.on_start_signal)
    
        def on_start_signal(self, argument):
            print("deuxième widget lancé !")
            print(argument)
    
    
        # lance le programme en python mais pour toi ça sera surement different.
        # Un truc commun c'est qu'il faut que instancier MainWindows
    if __name__ == "__main__":
        QT_app = QApplication(sys.argv)
    
        mainWindows = MainWindow()
    
        sys.exit(QT_app.exec_())
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/

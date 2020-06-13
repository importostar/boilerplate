---
title: grid (1)
date: 2020-05-07
---
Example Python program grid (1).py
This program creates a PyQt GUI

## Modules

* import itertools
* from PyQt5.QtCore import Qt
* from PyQt5.QtGui import QBrush
* from PyQt5.QtWidgets import (
* import sys

## Classes

* class Cell(QGraphicsRectItem):
* class Window(QMainWindow):

## Methods

* def __init__(self, *args, **kwargs):
* def mousePressEvent(self, event):
* def __init__(self, parent=None):
* def main():

## Code

Example Python PyQt program :

    # -*- coding:utf-8 -*-
    import itertools
    
    from PyQt5.QtCore import Qt
    from PyQt5.QtGui import QBrush
    from PyQt5.QtWidgets import (
        QApplication, QMainWindow,
        QGraphicsScene, QGraphicsView,
        QGraphicsRectItem,
    )
    
    
    class Cell(QGraphicsRectItem):
        def __init__(self, *args, **kwargs):
            super().__init__(*args, **kwargs)
            self.setBrush(QBrush(Qt.white))
            self.selected = False
    
        def mousePressEvent(self, event):
            if not self.selected:
                self.setBrush(QBrush(Qt.green))
                self.selected = True
            else:
                self.setBrush(QBrush(Qt.white))
                self.selected = False
    
    
    class Window(QMainWindow):
        def __init__(self, parent=None):
            super().__init__(parent)
            self.resize(600, 600)
    
            self.scene = QGraphicsScene(self)
            self.scene.setSceneRect(0, 0, 600, 600)
    
            self.view = QGraphicsView(self.scene)
            self.view.setBackgroundBrush(QBrush(Qt.gray))
            self.setCentralWidget(self.view)
    
            unit = 20
            rows, cols = range(self.width() // unit), range(self.height() // unit)
            for i, j in itertools.product(rows, cols):
                item = Cell(i*unit, j*unit, unit, unit)
                self.scene.addItem(item)
    
    
    def main():
        import sys
        app = QApplication(sys.argv)
        window = Window()
        window.show()
        sys.exit(app.exec_())
    
    
    if __name__ == "__main__":
        main()
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/

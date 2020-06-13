---
title: GSoCKanban
date: 2020-05-07
---
Example Python program GSoCKanban.py
This program creates a PyQt GUI

## Modules

* import sys
* from PyQt5.QtWidgets import QApplication, QWidget, QPushButton, QGridLayout
* from PyQt5.QtCore import Qt, QPoint

## Classes

* class App(QWidget):
* class DraggableButton(QPushButton):

## Methods

* def __init__(self):
* def init_ui(self):
* def __init__(self, text, parent, snap_pos):
* def mousePressEvent(self, event):
* def mouseMoveEvent(self, event):
* def main():

## Code

Example Python PyQt program :

    import sys
    from PyQt5.QtWidgets import QApplication, QWidget, QPushButton, QGridLayout
    from PyQt5.QtCore import Qt, QPoint
    
    
    class App(QWidget):
        def __init__(self):
            super(App, self).__init__()
            self.setWindowTitle("Kanban Board Demonstration")
            self.init_ui()
    
        def init_ui(self):
            window_x = 1280
            window_y = 800
            self.setGeometry(100, 100, window_x, window_y)
            grid = QGridLayout()
            grid.setParent(self)
            button = DraggableButton("Drag", self, QPoint(0, 100))
            button2 = DraggableButton("Drag2", self, QPoint(window_x/3, 100))
            button3 = DraggableButton("Drag3", self, QPoint(window_x/1.5, 100))
            button.move(0, 100)
            button2.move(window_x/3, 100)
            button3.move(window_x / 1.5, 100)
            self.setLayout(grid)
            grid.addWidget(button, 1, 1)
            grid.addWidget(button2, 1, 2)
            grid.addWidget(button3, 1, 3)
            self.show()
    
    
    class DraggableButton(QPushButton):
    
        def __init__(self, text, parent, snap_pos):
            super(DraggableButton, self).__init__(text, parent)
            self.move_pos = None
            self.snap_pos = snap_pos
    
        def mousePressEvent(self, event):
            if event.button() == Qt.LeftButton:
                self.move_pos = event.globalPos()
    
        def mouseMoveEvent(self, event):
            if event.buttons() == Qt.LeftButton:
                pos = self.pos()
                global_pos = event.globalPos()
                diff = global_pos - self.move_pos
                new_pos = pos + diff
                if abs(new_pos.x() - self.snap_pos.x()) <= 15 and abs(new_pos.y() - self.snap_pos.y() <= 15):
                    self.move(self.snap_pos)
                    return
                self.move(new_pos)
                self.move_pos = global_pos
    
    
    def main():
        app = QApplication(sys.argv)
        run_app = App()
        run_app.show()
        sys.exit(app.exec_())
    
    if __name__ == '__main__':
        main()
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/

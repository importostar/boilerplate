---
title: kanban
date: 2020-05-07
---
Example Python program kanban.py
This program creates a PyQt GUI

## Modules

* import sys
* from PyQt5.QtWidgets import *
* from PyQt5.QtCore import Qt

## Classes

* class DraggableTask(QFrame):
* class DraggableArea(QWidget):

## Methods

* def __init__(self,label,parent=None):
* def setupUI(self):
* def mousePressEvent(self,e):
* def dragMoved(self, e):
* def __init__(self, parent = None):
* def setupUI(self):
* def mouseReleaseEvent(self, e):
* def mouseMoveEvent(self, e):
* def main():

## Code

Example Python PyQt program :

    import sys
    from PyQt5.QtWidgets import *
    from PyQt5.QtCore import Qt
    
    class DraggableTask(QFrame):
    
        def __init__(self,label,parent=None):
            super(QFrame, self).__init__(parent)
            self.is_dragging = False
            self.start_x = 0
            self.start_y = 0
            self.name = label
            self.setupUI()
    
        def setupUI(self):
            self.layout = QVBoxLayout()
            self.setObjectName('task')
            self.title = QLabel(self.name)
            self.layout.addWidget(self.title)
            self.btn = QPushButton("Steps")
            self.layout.addWidget(self.btn)
            self.setLayout(self.layout)
            self.setStyleSheet('QFrame#task{border: 1px solid black;}')
            self.setMaximumSize(100,100)
    
        def mousePressEvent(self,e):
            if e.button() == Qt.LeftButton:
                self.is_dragging = True
                self.start_x = e.pos().x()
                self.start_y = e.pos().y()
    
        def dragMoved(self, e):
            mouse_pos = e.pos()
            dx = mouse_pos.x() - self.start_x
            dy = mouse_pos.y() - self.start_y
            btn_top = self.geometry()
            btn_top.moveTo(dx,dy)
            x = btn_top.x()
            y = btn_top.y()
            self.move(x,y)
    
    class DraggableArea(QWidget):
    
        def __init__(self, parent = None):
            super(QWidget, self).__init__(parent)
            self.setupUI()
    
        def setupUI(self):
            self.layout = QHBoxLayout()
            self.setLayout(self.layout)
            self.childItems = [ DraggableTask("Task 1"),
                                DraggableTask("Task 2"),
                                DraggableTask("Task 3")
            ]
            for item in self.childItems:
                self.layout.addWidget(item)
    
      
    
        def mouseReleaseEvent(self, e):
            for item in self.childItems:
                item.is_dragging = False
    
        def mouseMoveEvent(self, e):
            for item in self.childItems:
                if item.is_dragging:
                    item.dragMoved(e)
    
    
    def main():
        app = QApplication(sys.argv)
        w = QMainWindow()
        t = DraggableArea(w)
        w.setCentralWidget(t)
        w.setWindowTitle('Kanban GSOC demo')
        w.setGeometry(100,100,600,400)
        # w.resize(600,400)
        w.show()
        app.exec_()
    
    if __name__ == '__main__':
        main()
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/

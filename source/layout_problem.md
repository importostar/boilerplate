---
title: layout_problem
date: 2020-05-07
---
Example Python program layout_problem.py
This program creates a PyQt GUI

## Modules

* import sys
* from PyQt5.QtCore import Qt
* from PyQt5.QtWidgets import QApplication, QMainWindow, QWidget, QSlider, QScrollArea, QFrame, QPushButton
* from PyQt5.QtWidgets import QVBoxLayout, QHBoxLayout
* from vispy.scene import SceneCanvas, PanZoomCamera

## Classes

* class Left(QHBoxLayout):
* class Right(QFrame):
* class Viewer(QWidget):
* class Window:

## Methods

* def __init__(self):
* def __init__(self):
* def __init__(self):
* def __init__(self):
* def add_viewer(self):
* def resize(self, *args):
* def show(self):
* def main():

## Code

Example Python PyQt program :

    """This gist created to demonstrate an layout error, however, problem is solved with switching to anaconda/python
    """
    import sys
    from PyQt5.QtCore import Qt
    from PyQt5.QtWidgets import QApplication, QMainWindow, QWidget, QSlider, QScrollArea, QFrame, QPushButton
    from PyQt5.QtWidgets import QVBoxLayout, QHBoxLayout
    from vispy.scene import SceneCanvas, PanZoomCamera
    
    
    class Left(QHBoxLayout):
        def __init__(self):
            super().__init__()
            self.addWidget(QSlider(Qt.Vertical))
            self.addWidget(QSlider(Qt.Vertical))
    
    
    class Right(QFrame):
        def __init__(self):
            super().__init__()
            dim_buttons_layout = QHBoxLayout()
            dim_buttons_layout.addWidget(QPushButton("1D"))
            dim_buttons_layout.addWidget(QPushButton("2D"))
            dim_buttons_layout.addWidget(QPushButton("3D"))
    
            Right_layout = QVBoxLayout()
            Right_layout.addLayout(dim_buttons_layout)
            Right_layout.addWidget(QPushButton("asdF"))
            Right_layout.addWidget(QPushButton("fdsA"))
    
            self.setLayout(Right_layout)
    
    
    class Viewer(QWidget):
        def __init__(self):
            super().__init__()
            self.canvas = SceneCanvas(keys=None, vsync=True)
    
            layout = QVBoxLayout(self)
            layout.setContentsMargins(0, 0, 0, 0)
            self.setLayout(layout)
    
            # layout.addWidget(self.canvas.native)
    
            self.view = self.canvas.central_widget.add_view()
            self.view.camera = PanZoomCamera(aspect=1)
            self.view.camera.flip = (0, 1, 0)
            self.view.camera.set_range()
    
    
    class Window:
        def __init__(self):
            self._qt_window = QMainWindow()
            self._qt_central_widget = QWidget()
            self._qt_window.setCentralWidget(self._qt_central_widget)
            self._qt_central_widget.setLayout(QHBoxLayout())
            self._qt_window.statusBar().showMessage('Ready For Action')
    
        def add_viewer(self):
            left = Left()
            right = Right()
            viewer = Viewer()
            self._qt_central_widget.layout().addLayout(left)
            self._qt_central_widget.layout().addWidget(viewer)
            self._qt_central_widget.layout().addWidget(right)
    
        def resize(self, *args):
            self._qt_window.resize(*args)
    
        def show(self):
            self.resize(self._qt_window.layout().sizeHint())
            self._qt_window.show()
            self._qt_window.raise_()
    
    
    def main():
        win = Window()
        win.add_viewer()
        win.show()
        return win
    
    if __name__ == '__main__':
        application = QApplication(sys.argv)
        main_win = main()
        sys.exit(application.exec_())
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/

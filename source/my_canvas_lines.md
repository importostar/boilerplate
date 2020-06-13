---
title: my_canvas_lines
date: 2020-05-07
---
Example Python program my_canvas_lines.py
This program creates a PyQt GUI

## Modules

* import sys
* import numpy as np
* from PyQt5.QtWidgets import *
* from PyQt5.QtCore import QObject, QTimer, Qt, QPointF, QElapsedTimer 
* from PyQt5.QtCore import pyqtSlot as Slot
* from PyQt5.QtCore import pyqtSignal as Signal
* from PyQt5.QtGui import *
* """from PySide2.QtWidgets import *
* from PySide2.QtCore import *
* from PySide2.QtGui import *"""
* from vispy import scene

## Classes

* class Canvas(scene.SceneCanvas):
* class MainWindow(QMainWindow):

## Methods

* def __init__(self):
* def update_data(self, time, value):
* def __init__(self):
* def update_data(self):

## Code

Example Python PyQt program :

    import sys
    import numpy as np
    
    from PyQt5.QtWidgets import *
    from PyQt5.QtCore import QObject, QTimer, Qt, QPointF, QElapsedTimer 
    from PyQt5.QtCore import pyqtSlot as Slot
    from PyQt5.QtCore import pyqtSignal as Signal
    from PyQt5.QtGui import *
    
    """from PySide2.QtWidgets import *
    from PySide2.QtCore import *
    from PySide2.QtGui import *"""
    
    from vispy import scene
    
    
    class Canvas(scene.SceneCanvas):
        def __init__(self):
            scene.SceneCanvas.__init__(self)
            self.unfreeze()
            self.measure_fps()
    
            self.grid = self.central_widget.add_grid(spacing=0)
    
            padding_left = self.grid.add_widget(None, row=0, row_span=3, col=0)
            padding_left.width_min = 10
            padding_left.width_max = 20
    
            padding_right = self.grid.add_widget(None, row=0, row_span=3, col=3)
            padding_right.width_min = 10
            padding_right.width_max = 20
    
            padding_top = self.grid.add_widget(None, row=0, col=1, col_span=1)
            padding_top.height_min = 10
            padding_top.height_max = 20
    
            padding_bottom = self.grid.add_widget(None, row=3, col=1, col_span=1)
            padding_bottom.height_min = 20
            padding_bottom.height_max = 30
    
            self.y_axis = scene.AxisWidget(orientation='left')
            self.grid.add_widget(self.y_axis, row=1, col=1)
    
            self.x_axis = scene.AxisWidget(orientation='bottom',
                                            axis_label='Time (s)',
                                            tick_label_margin=15.0)
            self.grid.add_widget(self.x_axis, row=2, col=2)
    
            self.view = self.grid.add_view(row=1, col=2)
            self.view.camera = scene.MagnifyCamera(mag=1, size_factor=0.5, radius_ratio=0.6)
            self.y_axis.link_view(self.view)
            self.x_axis.link_view(self.view)
    
    
            self.data = np.zeros((3800,2))
    
    
            self.line = scene.Line(pos=self.data, parent=self.view.scene)
            self.view.camera.rect = (0, -1.1, 60, 2.2)
            #self.view.camera.set_range()
    
        def update_data(self, time, value):
    
            """translating and Updating time"""
            self.data[:-1, 0] = self.data[1:, 0] + time/1000.
            
            """translating values and adding the last measurement value"""
            self.data[:-1, 1] =  self.data[1:, 1]
            self.data[-1, 1] = value
    
            self.line.set_data(self.data)
        
    
    class MainWindow(QMainWindow):
        def __init__(self):
            QMainWindow.__init__(self)
            self.setWindowTitle("vispy test")
            self.canvas = Canvas()
            self.setCentralWidget(self.canvas.native)
            self.timer = QTimer()
            self.timer.timeout.connect(self.update_data)
            self.timer.start(16)
    
            self.elapsed_timer = QElapsedTimer()
            self.elapsed_timer.start()
    
    
        def update_data(self):
            value = np.array([np.sin(self.elapsed_timer.elapsed()/500)])
            self.canvas.update_data(16, value)
    
    if __name__ == "__main__":
        app = QApplication(sys.argv)
    
        window = MainWindow()
        window.show()
    
        sys.exit(app.exec_())
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/

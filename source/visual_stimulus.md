---
title: visual_stimulus
date: 2020-05-07
---
Example Python program visual_stimulus.py
This program creates a PyQt GUI

## Modules

* import sys
* from PyQt5.QtCore import *
* from PyQt5.QtGui import *
* from PyQt5.QtWidgets import *

## Classes

* class SSVEPWindow(QWidget):

## Methods

* def __init__(self):
* def set_stimuli(self, hz):
* def set_new_stimuli(self, value):
* def initUI(self):
* def change_color(self):

## Code

Example Python PyQt program :

    import sys
    from PyQt5.QtCore import *
    from PyQt5.QtGui import *
    from PyQt5.QtWidgets import *
    
    class SSVEPWindow(QWidget):
        def __init__(self):
            super().__init__()
            self.title = '画面チカチカ君'
            self.width = 1200
            self.height = 800
    
            # parameters
            self.timer = QTimer()
            self.timer.timeout.connect(self.change_color)
            self.light = False
    
            self.initUI()
    
        def set_stimuli(self, hz):
            self.stimuli_hz = hz
            self.stimuli_int_ms = 500 / self.stimuli_hz
            self.timer.setInterval(self.stimuli_int_ms)
            self.freq_text.setText('freq: {} Hz'.format(hz))
    
        def set_new_stimuli(self, value):
            self.set_stimuli(value / 10)
    
        def initUI(self):
            self.setWindowTitle(self.title)
            self.setGeometry(0, 0, self.width, self.height)
    
            # setup UI
            self.start_button = QPushButton('Start!!')
            self.start_button.clicked.connect(self.timer.start)
            self.stop_button = QPushButton('Stop...')
            self.stop_button.clicked.connect(self.timer.stop)
    
            self.paint_area = QWidget()
            self.paint_area.setAutoFillBackground(True)
    
            self.freq_slider = QSlider(Qt.Horizontal)
            self.freq_slider.setMinimum(10)
            self.freq_slider.setMaximum(200)
            self.freq_slider.valueChanged.connect(self.set_new_stimuli)
            self.freq_text = QLabel()
    
            self.layout = QGridLayout()
            self.layout.addWidget(self.start_button, 0, 0, 1, 3)
            self.layout.addWidget(self.stop_button, 0, 3, 1, 3)
            self.layout.addWidget(self.paint_area, 1, 0, 1, 6)
            self.layout.addWidget(self.freq_slider, 2, 0, 1, 5)
            self.layout.addWidget(self.freq_text, 2, 5, 1, 1)
            self.setLayout(self.layout)
    
            self.set_stimuli(1.0)
            self.change_color()
            self.show()
    
        def change_color(self):
            self.light = not self.light
            palette = QPalette()
            if self.light:
                palette.setColor(QPalette.Window, QColor(255,255,255))
            else:
                palette.setColor(QPalette.Window, QColor('black'))
            self.paint_area.setPalette(palette)
    
    if __name__ == '__main__':
        app = QApplication(sys.argv)
        gui = SSVEPWindow()
        sys.exit(app.exec_())
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/

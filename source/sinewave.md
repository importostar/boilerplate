---
title: sinewave
date: 2020-05-07
---
Example Python program sinewave.py
This program creates a PyQt GUI

## Modules

* from math import sin, pi
* from PyQt5.QtGui import QPainter, QPainterPath
* from PyQt5.QtWidgets import QWidget, QApplication, QSlider, QLabel

## Classes

* class Widget(QWidget):

## Methods

* def __init__(self, parent=None):
* def update_frequency(self, value):
* def update_amplitude(self, value):
* def get_y(self, x):
* def paintEvent(self, event):

## Code

Example Python PyQt program :

    from math import sin, pi
    
    from PyQt5.QtGui import QPainter, QPainterPath
    from PyQt5.QtWidgets import QWidget, QApplication, QSlider, QLabel
    
    
    class Widget(QWidget):
        def __init__(self, parent=None):
            super().__init__(parent)
    
            self.px_per_sec = 500
            self.freq_mult = 1 / 500
    
            self.freq_slider = QSlider(self)
            self.freq_slider.setRange(1, 60)
            self.freq_slider.valueChanged.connect(self.update_frequency)
            self.freq_label = QLabel(parent=self)
            self.freq_label.setGeometry(40, 0, 100, 20)
            self.update_frequency(self.freq_slider.value())
    
            self.amp_slider = QSlider(self)
            self.amp_slider.setRange(2, 50)
            self.amp_slider.valueChanged.connect(self.update_amplitude)
            self.amp_slider.move(20, 0)
            self.amp_label = QLabel(parent=self)
            self.amp_label.setGeometry(40, 20, 100, 20)
            self.update_amplitude(self.amp_slider.value())
    
        def update_frequency(self, value):
            self.frequency = value * self.freq_mult
            self.freq_label.setText(
                'Freq: {:0.0f}'.format(self.frequency * self.px_per_sec)
            )
            self.update()
    
        def update_amplitude(self, value):
            self.amplitude = value
            self.amp_label.setText('Amp: {}'.format(self.amplitude))
            self.update()
    
        def get_y(self, x):
            y = self.amplitude * sin(2 * pi * self.frequency * x)
            return y
    
        def paintEvent(self, event):
            painter = QPainter(self)
            painter.setRenderHint(QPainter.Antialiasing, True)
    
            x = 0
            while x <= self.width():
                painter.drawLine(x, 0, x, self.height())
                x += self.px_per_sec
    
            path = QPainterPath()
            for x in range(self.width()):
                y = self.get_y(x)
                path.lineTo(x, y + (self.height() / 2))
            painter.drawPath(path)
    
    
    if __name__ == '__main__':
        app = QApplication([])
        widget = Widget()
        widget.show()
        widget.resize(600, 300)
        app.exec_()

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/

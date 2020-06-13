---
title: qcolorbutton
date: 2020-05-07
---
Example Python program qcolorbutton.py
This program creates a PyQt GUI

## Modules

* from PyQt5.QtCore import pyqtSignal
* from PyQt5.QtGui import QColor, QPixmap, QIcon
* from PyQt5.QtWidgets import QColorDialog, QToolButton
* from PyQt5.QtWidgets import QApplication

## Classes

* class qColorButton(QToolButton):

## Methods

* def __init__(self, parent=None, color="#000", *args):
* def getColor(self):
* def setColor(self, color):
* def _onClicked(self):

## Code

Example Python PyQt program :

    #!/usr/bin/env python3
    # -*- coding: utf-8 -*-
    
    
    """qColorButton, use to configure colors, opens QColorDialog when clicked."""
    
    
    from PyQt5.QtCore import pyqtSignal
    
    from PyQt5.QtGui import QColor, QPixmap, QIcon
    
    from PyQt5.QtWidgets import QColorDialog, QToolButton
    
    
    class qColorButton(QToolButton):
    
        """Button, which is used for configuring colors."""
    
        colorChanged = pyqtSignal(QColor)  # Emit after current color has changed
    
        def __init__(self, parent=None, color="#000", *args):
            """Init class of qColorButton."""
            super(qColorButton, self).__init__(parent=None, *args)
            self.setColor(color if isinstance(color, QColor) else QColor())
            self.color, self.get_color = color, self.getColor
            self.clicked.connect(self._onClicked)
    
        def getColor(self):
            """Return current selected color."""
            return self.color
    
        def setColor(self, color):
            """Set a Color. Update button icon."""
            self.color = color
            c = self.color
            texts = (
                "HEXA #%02x%02x%02x%02x" % (
                    c.red(), c.green(), c.blue(), c.alpha()),
                "RGBA %d, %d, %d, %d" % (
                    c.red(), c.green(), c.blue(), c.alpha()))
            self.setText(texts[0])
            self.setToolTip("<b>" + "\n".join(texts))
            pixmap = QPixmap(self.iconSize())
            pixmap.fill(self.color)
            self.setIcon(QIcon(pixmap))
            self.colorChanged.emit(self.color)
    
        def _onClicked(self):
            """Button has been clicked. Show dialog and update color."""
            color = QColorDialog.getColor()
            if color.isValid():
                self.setColor(color)
    
    
    if __name__ in "__main__":
        from PyQt5.QtWidgets import QApplication
        app = QApplication([])
        numberPad = qColorButton(None, "#bebe")
        numberPad.show()
        exit(app.exec_())
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/

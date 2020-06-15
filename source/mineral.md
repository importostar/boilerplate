---
title: mineral
date: 2020-05-07
---
Example Python program mineral.py

## Modules

* from functools import partial
* from PyQt5.QtCore import pyqtProperty, Qt, QVariant
* from PyQt5.QtWidgets import QFormLayout, QSlider, QStyledItemDelegate, QFrame

## Classes

* class MineralLevelsEditor(QFrame):
* class MineralLevelsDelegate(QStyledItemDelegate):

## Methods

* def __init__(self, parent=None):
* def levels(self):
* def levels(self, levels):
* def _setLevel(self, mineral, level):
* def createEditor(self, parent, option, index):
* def updateEditorGeometry(self, editor, option, index):

## Code

Example Python PyQt program :

    from functools import partial
    
    from PyQt5.QtCore import pyqtProperty, Qt, QVariant
    from PyQt5.QtWidgets import QFormLayout, QSlider, QStyledItemDelegate, QFrame
    
    
    class MineralLevelsEditor(QFrame):
    
        def __init__(self, parent=None):
            super(MineralLevelsEditor, self).__init__(parent)
    
            self._levels = None
    
            self.setAutoFillBackground(True)
            self.setFrameStyle(QFrame.StyledPanel | QFrame.Raised)
            self.setLayout(QFormLayout())
    
        @pyqtProperty(QVariant, user=True)
        def levels(self):
            return self._levels
    
        @levels.setter
        def levels(self, levels):
    
            self._levels = levels
    
            for mineral, level in levels.items():
                slider = QSlider(Qt.Horizontal)
                slider.setMinimum(0)
                slider.setMaximum(100)
                slider.setValue(level)
                slider.valueChanged.connect(partial(self._setLevel, mineral))
                self.layout().addRow(mineral + ':', slider)
    
        def _setLevel(self, mineral, level):
            self._levels[mineral] = level
    
    
    class MineralLevelsDelegate(QStyledItemDelegate):
    
        def createEditor(self, parent, option, index):
            return MineralLevelsEditor(parent)
    
        def updateEditorGeometry(self, editor, option, index):
            editor.setGeometry(
                option.rect.x(), option.rect.y() + option.rect.height(),
                editor.sizeHint().width(), editor.sizeHint().height())

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/

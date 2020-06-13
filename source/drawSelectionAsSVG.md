---
title: drawSelectionAsSVG
date: 2020-05-07
---
Example Python program drawSelectionAsSVG.py

## Modules

* from defconQt.tools import drawing
* from PyQt5.QtCore import QRect, QSize, Qt
* from PyQt5.QtGui import QPainter
* from PyQt5.QtSvg import QSvgGenerator
* from PyQt5.QtWidgets import QApplication, QFileDialog
* import os

## Methods

* def _currentFontSelection():

## Code

Example Python PyQt program :

    from defconQt.tools import drawing
    from PyQt5.QtCore import QRect, QSize, Qt
    from PyQt5.QtGui import QPainter
    from PyQt5.QtSvg import QSvgGenerator
    from PyQt5.QtWidgets import QApplication, QFileDialog
    import os
    
    def _currentFontSelection():
        """
        We should probably have font.selection sometimes, but for now this will do.
        """
        app = QApplication.instance()
        window = app.currentMainWindow()
        if window is None:
            return set()
        widget = window.glyphCellView
        return widget.glyphsForIndexes(widget.selection())
    
    selection = _currentFontSelection()
    
    if selection:
        path = QFileDialog.getExistingDirectory()
        if path:
            for glyph in selection:
                if None not in (glyph, glyph.bounds):
                    generator = QSvgGenerator()
                    generator.setFileName(os.path.join(path, "%s.svg" % glyph.name))
                    font = glyph.font
                    width = glyph.width
                    if font is not None:
                        ascender = font.info.ascender
                        height = font.info.unitsPerEm
                    else:
                        _, top, _, bottom = glyph.bounds
                        ascender = height = top - bottom
                    generator.setSize(QSize(width, height))
                    generator.setViewBox(QRect(0, 0, width, height))
                    painter = QPainter()
                    painter.begin(generator)
                    painter.translate(0, ascender)
                    painter.scale(1, -1)
                    drawing.drawGlyphFillAndStroke(painter, glyph, 1.0, (0, 0, 0, 0), drawStroke=False, contourFillColor=Qt.black)
                    #drawing.drawGlyphPoints(painter, glyph, 1.0, (0, 0, 0, 0))
                    painter.end()

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/

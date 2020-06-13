---
title: drawAsSVG
date: 2020-05-07
---
Example Python program drawAsSVG.py

## Modules

* from defconQt.tools import drawing
* from PyQt5.QtCore import QRect, QSize
* from PyQt5.QtGui import QPainter
* from PyQt5.QtSvg import QSvgGenerator
* from PyQt5.QtWidgets import QFileDialog

## Code

Example Python PyQt program :

    from defconQt.tools import drawing
    from PyQt5.QtCore import QRect, QSize
    from PyQt5.QtGui import QPainter
    from PyQt5.QtSvg import QSvgGenerator
    from PyQt5.QtWidgets import QFileDialog
    
    glyph = CurrentGlyph()
    
    if None not in (glyph, glyph.bounds):
        path, _ = QFileDialog.getSaveFileName(None, "Save As SVG","", "SVG file (*.svg)")
        if path:
            generator = QSvgGenerator()
            generator.setFileName(path)
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
            drawing.drawGlyphFillAndStroke(painter, glyph, 1.0, (0, 0, 0, 0))
            drawing.drawGlyphPoints(painter, glyph, 1.0, (0, 0, 0, 0))
            painter.end()

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/

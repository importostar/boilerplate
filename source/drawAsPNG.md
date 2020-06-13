---
title: drawAsPNG
date: 2020-05-07
---
Example Python program drawAsPNG.py
Python version 3.x or newer.
To check the Python version use:

    python --version

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
        cache = []  # gc
        if path:
            file = open(os.path.join(path, "nam.txt"), "wt")
            for glyph in selection:
                if None not in (glyph, glyph.bounds):
                    pixmap = glyph.getRepresentation("defconQt.GlyphCell", width=512, height=512, drawHeader=False, drawMetrics=False)
                    pixmap.save(os.path.join(path, "%s.png" % glyph.name))
                    cache.append(pixmap)
                    print(glyph.name, file=file)
            file.close()

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/

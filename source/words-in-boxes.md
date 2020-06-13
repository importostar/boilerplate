---
title: words in boxes
date: 2020-05-07
---
Example Python program words-in-boxes.py
This program creates a PyQt GUI
For Python version 2.x.
To test your Python version use:

    python --version

## Modules

* import sys
* import time
* from PyQt5.QtWidgets import *
* from PyQt5.QtCore import *
* from PyQt5.QtGui import *

## Classes

* class WordPainter(QWidget):

## Methods

* def on_paint(event, painter):
* def paint_words(words, painter, x, y):
* def paint_word(text, painter, x, y):
* def __init__(self, on_paint_fn):
* def paintEvent(self, event):

## Code

Example Python PyQt program :

    #!/usr/bin/env python
    
    # a pyqt script which draws words inside of rounded rectangles.
    
    # see https://doc.qt.io/qt-5/qpainter.html
    # see http://pyqt.sourceforge.net/Docs/PyQt5/api/qpen.html
    
    import sys
    import time
    from PyQt5.QtWidgets import *
    from PyQt5.QtCore import *
    from PyQt5.QtGui import *
    
    
    words = ["hello", "world", "these", "are", "words", "in", "boxes"]
    
    
    # this function will be called on every paint event.
    def on_paint(event, painter):
        # fill the canvas with white
        painter.fillRect(event.rect(), QBrush(Qt.white))
        # paint the words
        (x, y) = (20, 20)
        paint_words(words, painter, x, y)
    
    
    # paint the words in boxes, all in a single row.
    def paint_words(words, painter, x, y):
        pad = 5
        # draw the words in boxes, all in a row.
        for word in words:
            (width, height) = paint_word(word, painter, x, y)
            x += (width + pad)
    
    
    # paint a word inside of a box, starting at (x, y)
    # returns the (width, height) used to paint the word.
    def paint_word(text, painter, x, y):
        text_pad = 5
        text_top_fudge = -2  # qt text seems to have extra padding on top.
        corner_radius = 4
        # calculate the size of the text
        text_bounds = QFontMetrics(painter.font()).boundingRect(text)
        # configure the box stroke
        pen = QPen()
        pen.setColor(Qt.red)
        pen.setWidth(1)
        painter.setPen(pen)
        # configure the box fill
        painter.setBrush(QBrush(QColor(255,192,192,255)))  # light red
        # draw the box
        # note: the rounded corners come out a bit odd.
        # see https://stackoverflow.com/questions/6507511/qt-round-rectangle-why-corners-are-different
        painter.drawRoundedRect(
            x,
            y,
            text_bounds.width() + (text_pad * 2),
            text_bounds.height() + (text_pad * 2),
            corner_radius,
            corner_radius
        )
        # configure the text stroke
        pen = QPen() # defaults to black
        painter.setPen(pen)
        # draw the text
        painter.drawText(
            x + text_pad,
            y + text_bounds.height() + text_pad + text_top_fudge,
            text
        )
        return (
            text_bounds.width() + (text_pad * 2),
            text_bounds.height() + (text_pad * 2)
        )
    
    
    # a widget which paints words inside of boxes
    class WordPainter(QWidget):
        def __init__(self, on_paint_fn):
            QWidget.__init__(self)
            self.on_paint_fn = on_paint_fn
        
        # this gets called every time the widget needs to repaint (e.g. window resize)
        def paintEvent(self, event):
            then = time.time()
            painter = QPainter()
            painter.begin(self)
            self.on_paint_fn(event, painter)
            painter.end()
            now = time.time()
            elapsed = now - then
            print "elapsed: %s" % elapsed
            print "fps: %s" % (1.0/elapsed)
    
    
    if __name__ == "__main__":
        app = QApplication(sys.argv)
        window = WordPainter(on_paint)
        window.show()
        sys.exit(app.exec_())

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/

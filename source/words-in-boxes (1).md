---
title: words in boxes (1)
date: 2020-05-07
---
Example Python program words-in-boxes (1).py
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
* def paint_json(js, painter, x, y, pad=5):
* def paint_word_in_box(text, painter, x, y, rgb, pad=5):
* def paint_box(painter, x, y, w, h, rgb):
* def lighter_rgb(rgb):
* def size_of_json(js, painter, pad=5):
* def size_of_word_in_box(text, painter, pad=5):
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
    
    
    json_root = ["hello", "world", ["these", "are"], "words", "in", "boxes"]
    
    
    word_rgb = (0,0,255)
    array_rgb = (0,255,0)
    
    
    # this function will be called on every paint event.
    def on_paint(event, painter):
        # fill the canvas with white
        painter.fillRect(event.rect(), QBrush(Qt.white))
        # paint the words
        (x, y) = (20, 20)
        paint_json(json_root, painter, x, y)
    
    
    # recursively paint a json structure, starting at (x,y).
    # returns the (width, height) used to paint the word.
    def paint_json(js, painter, x, y, pad=5):
        if isinstance(js, list):
            # first, paint the container box
            (w, h) = size_of_json(js, painter, pad)
            paint_box(painter, x, y, w, h, array_rgb)
            # now paint the elements inside of the box
            for j in js:
                x += pad
                (jw, jh) = size_of_json(j, painter, pad)
                paint_json(j, painter, x, y + ((h-jh)/2), pad)
                x += jw
            return (w, h)
        else:
            return paint_word_in_box("%s" % js, painter, x, y, word_rgb, pad)
    
    
    # paint a word inside of a box, starting at (x, y).
    # returns the (width, height) used to paint the word.
    def paint_word_in_box(text, painter, x, y, rgb, pad=5):
        # calculate the size of the text
        text_bounds = QFontMetrics(painter.font()).boundingRect(text)
        w = pad + text_bounds.width() + pad
        h = pad + text_bounds.height() + pad
        paint_box(painter, x, y, w, h, rgb)
        # configure the text stroke
        pen = QPen() # defaults to black
        painter.setPen(pen)
        # draw the text
        text_top_fudge = -2  # qt text seems to have extra padding on top.
        baseline = y + text_bounds.height() + pad + text_top_fudge
        painter.drawText(
            pad + x,
            baseline,
            text
        )
        return (w, h)
    
    
    # paint a box (with a border stroke and rounded corners)
    def paint_box(painter, x, y, w, h, rgb):
        corner_radius = 4
        # configure the box stroke
        pen = QPen()
        (r,g,b) = rgb
        pen.setColor(QColor(r,g,b,255))
        pen.setWidth(1)
        painter.setPen(pen)
        # configure the box fill
        (r,g,b) = lighter_rgb(rgb)
        painter.setBrush(QBrush(QColor(r,g,b,255)))
        # draw the box
        # note: the rounded corners come out a bit odd.
        # see https://stackoverflow.com/questions/6507511/qt-round-rectangle-why-corners-are-different
        painter.drawRoundedRect(
            x, y, w, h,
            corner_radius,
            corner_radius
        )
    
    
    # return a lighter version of a color
    def lighter_rgb(rgb):
        (r,g,b) = rgb
        return (
            min(255, int(r + ((255-r)/1.15))),
            min(255, int(g + ((255-g)/1.15))),
            min(255, int(b + ((255-b)/1.15))),
        )
    
    
    # calculate the bounding box size of a json structure
    def size_of_json(js, painter, pad=5):
        if isinstance(js, list):
            total_w = pad
            total_h = 0
            for j in js:
                (w, h) = size_of_json(j, painter, pad)
                total_w += (w + pad)
                total_h = max(total_h, h)
            return (total_w, pad + total_h + pad)
        else:
            return size_of_word_in_box("%s" % js, painter, pad)
    
    
    # calculate the bounding box size of a word in a box
    def size_of_word_in_box(text, painter, pad=5):
        text_bounds = QFontMetrics(painter.font()).boundingRect(text)
        w = pad + text_bounds.width() + pad
        h = pad + text_bounds.height() + pad
        return (w, h)
    
    
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

---
title: json renderer
date: 2020-05-07
---
Example Python program json-renderer.py
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

* def qcolor(rgb):
* def lighter(rgb):
* def on_paint(event, painter):
* def paint_json(js, painter, x, y, pad=5):
* def paint_array(arr, painter, x, y, pad=5):
* def paint_dictionary(d, painter, x, y, pad=5):
* def paint_kv_pair((k,v), painter, x, y, link_rgb, pad=5):
* def paint_word_in_box(text, painter, x, y, rgb, border_rgb, pad=5):
* def paint_box(painter, x, y, w, h, rgb, border_rgb):
* def size_of_json(js, painter, pad=5):
* def size_of_kv_pair((k,v), painter, pad=5):
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
    
    
    json_root = ["hello", ["world", ["these", "are"]], {"a": 1, "b": 2}, "words", "in", "boxes"]
    
    
    # given an rgb triple, return s QColor
    def qcolor(rgb):
        (r,g,b) = rgb
        return QColor(r,g,b,255)
    
    
    # return a lighter version of a color
    def lighter(rgb):
        (r,g,b) = rgb
        return (
            min(255, int(r + ((255-r)/1.15))),
            min(255, int(g + ((255-g)/1.15))),
            min(255, int(b + ((255-b)/1.15))),
        )
    
    
    colors = {
        "bg": (255,255,255),
        "word_border": (0,0,0),
        "word": (255,255,255),
        "array_border": (0,0,255),
        "array": lighter((0,0,255)),
        "dict_border": (255,0,0),
        "dict": lighter((255,0,0))
    }
    
    
    # this function will be called on every paint event.
    def on_paint(event, painter):
        # fill the canvas with white
        painter.fillRect(event.rect(), QBrush(qcolor(colors["bg"])))
        # paint the words
        (x, y) = (20, 20)
        paint_json(json_root, painter, x, y)
    
    
    # recursively paint a json structure, starting at (x,y).
    # returns the (width, height) used to paint the json structure.
    def paint_json(js, painter, x, y, pad=5):
        if isinstance(js, list):
            return paint_array(js, painter, x, y, pad)
        elif isinstance(js, dict):
            return paint_dictionary(js, painter, x, y, pad)
        else:
            return paint_word_in_box(
                "%s" % js, painter, x, y, colors["word"], colors["word_border"], pad
            )
    
    
    # paint the items of the array in a container box.
    # returns the (width, height) used to paint the array.
    def paint_array(arr, painter, x, y, pad=5):
        # first, paint the container box
        (w, h) = size_of_json(arr, painter, pad)
        paint_box(painter, x, y, w, h, colors["array"], colors["array_border"])
        # now paint the elements inside of the box
        y += pad
        for j in arr:
            x += pad
            (jw, jh) = size_of_json(j, painter, pad)
            # paint_json(j, painter, x, y + ((h-jh)/2.0), pad)
            paint_json(j, painter, x, y, pad)
            x += jw
        return (w, h)
    
    
    # paint the key-value pairs of the dictionary in a container box.
    # returns the (width, height) used to paint the dictionary.
    def paint_dictionary(d, painter, x, y, pad=5):
        # first, paint the container box
        (w, h) = size_of_json(d, painter, pad)
        paint_box(painter, x, y, w, h, colors["dict"], colors["dict_border"])
        # now paint the key-value pairs inside the box
        y += pad
        for k in sorted(d.keys()):
            v = d[k]
            x += pad
            (iw, ih) = size_of_kv_pair((k,v), painter, pad)
            paint_kv_pair((k,v), painter, x, y, colors["word_border"], pad)
            x += iw
        return (w, h)
    
    
    # paint a linked key-value pair inside a linked pair of boxes.
    # returns the (width, height) used to paint the pair.
    def paint_kv_pair((k,v), painter, x, y, link_rgb, pad=5):
        (kw, kh) = size_of_json(k, painter, pad)
        (vw, vh) = size_of_json(v, painter, pad)
        paint_json(k, painter, x, y, pad)
        paint_json(v, painter, x + kw + pad, y, pad)
        # paint the link between the two boxes
        # configure the box stroke
        pen = QPen()
        pen.setColor(qcolor(link_rgb))
        pen.setWidth(1)
        painter.setPen(pen)
        painter.drawLine(
            x + kw,  y + (kh/2.0),
            x + kw + pad,  y + (kh/2.0)
        )
    
    
    # paint a word inside of a box, starting at (x, y).
    # returns the (width, height) used to paint the word.
    def paint_word_in_box(text, painter, x, y, rgb, border_rgb, pad=5):
        # calculate the size of the text
        text_bounds = QFontMetrics(painter.font()).boundingRect(text)
        w = pad + text_bounds.width() + pad
        h = pad + text_bounds.height() + pad
        paint_box(painter, x, y, w, h, rgb, border_rgb)
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
    def paint_box(painter, x, y, w, h, rgb, border_rgb):
        corner_radius = 4
        # configure the box stroke
        pen = QPen()
        pen.setColor(qcolor(border_rgb))
        pen.setWidth(1)
        painter.setPen(pen)
        # configure the box fill
        painter.setBrush(QBrush(qcolor(rgb)))
        # draw the box
        # note: the rounded corners come out a bit odd.
        # see https://stackoverflow.com/questions/6507511/qt-round-rectangle-why-corners-are-different
        painter.drawRoundedRect(
            x, y, w, h,
            corner_radius,
            corner_radius
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
        elif isinstance(js, dict):
            total_w = pad
            total_h = 0
            for k in sorted(js.keys()):
                v = js[k]
                (w, h) = size_of_kv_pair((k,v), painter, pad)
                total_w += (w + pad)
                total_h = max(total_h, h)
            return (total_w, pad + total_h + pad)
        else:
            return size_of_word_in_box("%s" % js, painter, pad)
    
    
    # calculate the bounding box size of one key-value pair
    def size_of_kv_pair((k,v), painter, pad=5):
        (kw, kh) = size_of_json(k, painter, pad)
        (vw, vh) = size_of_json(v, painter, pad)
        return (
            kw + pad + vw,
            max(kh, vh)
        )
    
    
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
            # hmm, these don't seem to do anything?
            # painter.setRenderHint(QPainter.TextAntialiasing, True)
            # painter.setRenderHint(QPainter.Antialiasing, True)
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
    
    # todo:
    # look into painting to a QImage, and then painting that with QPainter.
    # perhaps that can be a higher-performance "compositing" option?
    # (tradeoff less cpu for more memory usage?)
    
    # todo:
    # cache all of the calculated sizes of objects
    # note: this could be simpler/faster with monospaced fonts
    
    # todo:
    # line-wrapping?
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/

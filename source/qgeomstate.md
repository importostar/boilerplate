---
title: qgeomstate
date: 2020-05-07
---
Example Python program qgeomstate.py
This program creates a PyQt GUI

## Modules

* import struct
* from collections import namedtuple
* from PyQt5.QtCore import Qt, QRect, QMargins
* from PyQt5.QtWidgets import QWidget
* import unittest
* from PyQt5.QtWidgets import QApplication
* from PyQt5.QtCore import Qt, QByteArray, QPoint, QRect, QSize

## Classes

* class TestGeometryRestore(unittest.TestCase):

## Methods

* def geom_state(magic, major_version, *args, **kwargs):
* def geom_state_from_bytes(state):
* def geom_state_to_bytes(parsedstate):
* def geom_state_normal(state, widget_or_margins=None):
* def frame_margins(widget):
* def setUp(self):
* def test_pack(self):
* def test_unpack(self):
* def test_restore_to_normal(self):

## Code

Example Python PyQt program :

    """
    Utilities for inspecting/modifying widget geometry state as returned/set by
    `QWidget.saveGeometry` and `QWidget.restoreGeometry`
    
    """
    
    import struct
    from collections import namedtuple
    
    #: Parsed geometry state (version 1; Qt < 5.4)
    _geom_state_v1 = namedtuple(
        "geom_state",
        ["magic",   # int32_t magic constant
         "major_version", "minor_version",  # (uint16_t, uint16_t) format version
         #: 4x int32_t ( == frameGeometry().getCoords())
         "frame_left", "frame_top", "frame_right", "frame_bottom",
         #: 4x int32_t ( == geometry().getCoords() WHEN NOT in FullScreen)
         "normal_left", "normal_top", "normal_right", "normal_bottom",
         "screen",      # screen number
         "maximized",   # windowState() & Qt.WindowMaximized
         "full_screen"  # windowState() & Qt.WindowFullScreen
         ]
    )
    
    
    #: Parsed geometry state (version 2; Qt >= 5.4)
    _geom_state_v2 = namedtuple(
        "geom_state",
        _geom_state_v1._fields +
        ("screen_width", )  # int32_t screen's width
    )
    
    
    def geom_state(magic, major_version, *args, **kwargs):
        if magic != geom_state.MAGIC:
            raise ValueError
    
        if major_version == 1:
            return geom_state.v1(magic, major_version, *args, **kwargs)
        elif major_version == 2:
            return geom_state.v2(magic, major_version, *args, **kwargs)
        else:
            raise ValueError
    
    geom_state.MAGIC = 0x1D9D0CB
    geom_state.v1 = _geom_state_v1
    geom_state.v2 = _geom_state_v2
    
    
    def geom_state_from_bytes(state):
        """
        Parse the `QWidget.saveGeometry` return value
    
        Parameters
        ----------
        state : bytes
            Saved widget geometry state as returned by :func:`QWidget.saveGeometry`
    
        Returns
        -------
        parsed : namedtuple
            The parsed geometry state as a named tuple
        """
        state = bytes(state)
        MAGIC = 0x1D9D0CB
        header_fmt = (
            "I"   # magic number
            "HH"  # minor.major format version
        )
        header_len = struct.calcsize(">" + header_fmt)
        magic, major, minor = struct.unpack(">" + header_fmt, state[:header_len])
        if magic != MAGIC:
            raise ValueError("Magic value does not match")
        if major not in {1, 2}:
            raise ValueError("Do not know how to handle version {}".format(major))
    
        payload_fmt = (
            "4i4i"  # 2x QRect's left, top, right, bottom
            "i"     # screen number
            "B"     # windowState() & Qt.WindowMaximized
            "B"     # windowState() & Qt.WindowFullScreen
        )
    
        if major == 2:
            payload_fmt += "i"  # screen's width
    
        payload_len = struct.calcsize(payload_fmt)
        geom = struct.unpack(
            ">" + payload_fmt, state[header_len: header_len + payload_len])
        return geom_state(magic, major, minor, *geom)
    
    
    def geom_state_to_bytes(parsedstate):
        """
        Pack a parsed geometry state (geom_state) representation back to bytes
    
        Parameters
        ----------
        parsedstate : geom_state
    
        Returns
        -------
        bytes : bytes
        """
        fmt = ">IHH4i4iiBB"
        _, major = parsedstate[:2]
        if major >= 2:
            fmt += "i"
    
        return struct.pack(fmt, *parsedstate)
    
    geom_state.from_bytes = geom_state_from_bytes
    geom_state.v1.to_bytes = geom_state_to_bytes
    geom_state.v2.to_bytes = geom_state_to_bytes
    
    
    from PyQt5.QtCore import Qt, QRect, QMargins
    from PyQt5.QtWidgets import QWidget
    
    
    def geom_state_normal(state, widget_or_margins=None):
        """
        Strip the full screen flags from `state` returning it into normal mode
    
        Should be somewhat equivalent to .showNormal()
    
        Parameters
        ----------
        state : geom_state
            Parsed geometry state
        widget_or_margins : Union[QWidget, QMargins, Tuple[int, int, int, int]]
            Window frame margin hints
    
        Returns
        -------
        state : geom_state
        """
        def frame_margins(widget):
            frame = widget.frameGeometry()
            geom = widget.geometry()
            return (frame.left() - geom.left(),
                    frame.top() - geom.top(),
                    frame.right() - geom.right(),
                    frame.bottom() - frame.bottom())
    
        if state.full_screen:
            # When a widget is in maximized/full screen mode the normal geometry
            # (as stored by saveGeometry) contains the widget's .geometry()
            # *before* it went to maximized/full screen (i.e. the geometry it
            # would/will get when restored back to normal mode). We use that to
            # recreate the frame geometry for the normal mode.
            frame = QRect()
            frame.setCoords(state.frame_left, state.frame_top,
                            state.frame_right, state.frame_bottom)
            normal = QRect()
            normal.setCoords(state.normal_left, state.normal_top,
                             state.normal_right, state.normal_bottom)
    
            if widget_or_margins is None:
                margins = 1, 20, 1, 1  # better guess?
            elif isinstance(widget_or_margins, QWidget):
                margins = frame_margins(widget_or_margins)
            elif isinstance(widget_or_margins, QMargins):
                margins = widget_or_margins
                margins = (margins.left(), margins.top(),
                           margins.right(), margins.bottom())
            else:
                margins = widget_or_margins
    
            left, top, right, bottom = margins
            frame = normal.adjusted(-left, -top, right, bottom)
    
            state = state._replace(
                frame_left=frame.left(), frame_top=frame.top(),
                frame_right=frame.right(), frame_bottom=frame.bottom(),
                full_screen=0, maximized=0
            )
        return state
    
    
    import unittest
    
    from PyQt5.QtWidgets import QApplication
    from PyQt5.QtCore import Qt, QByteArray, QPoint, QRect, QSize
    
    
    class TestGeometryRestore(unittest.TestCase):
        def setUp(self):
            app = QApplication.instance()
            if not app:
                app = QApplication([])
            self.app = app
    
        def test_pack(self):
            w = QWidget()
            geom = geom_state(
                geom_state.MAGIC, 1, 0,
                50, 50, 99, 99,  # frame geom
                50, 70, 99, 99,  # normal geom
                0, 0, 0    # screen, maximized, fullscreen
            )
            w.restoreGeometry(QByteArray(geom.to_bytes()))
            self.assertEqual(w.frameGeometry().topLeft(), QPoint(50, 50))
            self.assertEqual(w.geometry().size(), QSize(50, 30))
    
            self.assertEqual(geom, geom_state.from_bytes(geom.to_bytes()))
    
        def test_unpack(self):
            w = QWidget()
            w.setGeometry(QRect(50, 50, 50, 30))
            w.move(50, 50)
            state = geom_state.from_bytes(bytes(w.saveGeometry()))
            self.assertEqual(state.frame_top, 50)
            self.assertEqual(state.frame_left, 50)
            self.assertEqual(state.maximized, 0)
            self.assertEqual(state.full_screen, 0)
    
            w.setWindowState(w.windowState() | Qt.WindowFullScreen)
            state = geom_state.from_bytes(bytes(w.saveGeometry()))
            self.assertEqual(state.full_screen, Qt.WindowFullScreen)
            self.assertEqual(state.maximized, 0)
    
            w.setWindowState(w.windowState() ^ Qt.WindowFullScreen)
            w.setWindowState(w.windowState() | Qt.WindowMaximized)
            state = geom_state.from_bytes(bytes(w.saveGeometry()))
            self.assertEqual(state.full_screen, 0)
            self.assertEqual(state.maximized, Qt.WindowMaximized)
    
        def test_restore_to_normal(self):
            geom = geom_state(
                geom_state.MAGIC, 1, 0,
                0, 0, 200, 200,
                50, 70, 99, 99,
                0, 0, Qt.WindowFullScreen
            )
            normal = geom_state_normal(geom, (0, 20, 0, 0))
            self.assertEqual(normal.full_screen, 0)
            self.assertEqual(normal.maximized, 0)
            self.assertEqual(normal.frame_left, 50)
            self.assertEqual(normal.frame_top, 50)
            self.assertEqual(normal.frame_bottom, 99)
            self.assertEqual(normal.frame_right, 99)
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/

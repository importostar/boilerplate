---
title: QGraphicsScene_00_draw_grid
date: 2020-05-07
---
Example Python program QGraphicsScene_00_draw_grid.py
This program creates a PyQt GUI
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import sys
* from PyQt5 import QtWidgets
* from PyQt5 import QtCore
* from PyQt5 import QtGui
* from PyQt5.QtWidgets import QMenu
* from PyQt5.QtCore import QEvent
* from PyQt5.QtGui import QKeySequence
* from PyQt5.QtGui import QPen, QColor
* from PyQt5.QtCore import Qt
* from PyQt5.QtGui import QCursor
* import enum
* from PyQt5.QtWidgets import QGraphicsSceneMouseEvent

## Classes

* class Settings(enum.Enum):
* class QS(QtWidgets.QGraphicsScene):
* class QV(QtWidgets.QGraphicsView):

## Methods

* def create_action(parent, text, slot=None,
* def __init__(self, *args, **kwargs):
* def mouseMoveEvent(self, event:QGraphicsSceneMouseEvent):
* def mouseReleaseEvent(self, event:QGraphicsSceneMouseEvent):
* def draw_grid(self):
* def set_visible(self,visible=True):
* def delete_grid(self):
* def set_opacity(self,opacity):
* def __init__(self, *args, **kwargs):
* def create_actions(self):
* def get_coords(self):
* def on_zoom_in(self):
* def on_zoom_out(self):
* # def drawBackground(self, painter, rect):

## Code

Example Python PyQt program :

    import sys
    from PyQt5 import QtWidgets
    from PyQt5 import QtCore
    from PyQt5 import QtGui
    from PyQt5.QtWidgets import QMenu
    from PyQt5.QtCore import QEvent
    from PyQt5.QtGui import QKeySequence
    from PyQt5.QtGui import QPen, QColor
    from PyQt5.QtCore import Qt
    from PyQt5.QtGui import QCursor
    
    import enum
    
    from PyQt5.QtWidgets import QGraphicsSceneMouseEvent
    
    def create_action(parent, text, slot=None,
                      shortcut=None, shortcuts=None, shortcut_context=None,
                      icon=None, tooltip=None,
                      checkable=False, checked=False):
        action = QtWidgets.QAction(text, parent)
    
        if icon is not None:
            action.setIcon(QIcon(':/%s.png' % icon))
        if shortcut is not None:
            action.setShortcut(shortcut)
        if shortcuts is not None:
            action.setShortcuts(shortcuts)
        if shortcut_context is not None:
            action.setShortcutContext(shortcut_context)
        if tooltip is not None:
            action.setToolTip(tooltip)
            action.setStatusTip(tooltip)
        if checkable:
            action.setCheckable(True)
        if checked:
            action.setChecked(True)
        if slot is not None:
            action.triggered.connect(slot)
    
        return action
    
    
    class Settings(enum.Enum):
        WIDTH = 20
        HEIGHT = 15
        NUM_BLOCKS_X = 10
        NUM_BLOCKS_Y = 14
    
    
    class QS(QtWidgets.QGraphicsScene):
    
        def __init__(self, *args, **kwargs):
            super().__init__(*args, **kwargs)
    
            self.lines = []
            self.l = []
            self.draw_grid()
            self.set_opacity(0.3)
            #self.set_visible(False)
            #self.delete_grid()
    
        def mouseMoveEvent(self, event:QGraphicsSceneMouseEvent):
            x = event.scenePos().x()
            y = event.scenePos().y()
            codx, cody = x // Settings.WIDTH.value, y // Settings.HEIGHT.value
            print(x, y, codx, cody)
    
        def mouseReleaseEvent(self, event:QGraphicsSceneMouseEvent):
            x = event.scenePos().x()
            y = event.scenePos().y()
            codx, cody = x // Settings.WIDTH.value, y // Settings.HEIGHT.value
            pen = QPen(QColor(255, 0, 100), 1, Qt.SolidLine)
            self.l.append(
                # - 5를 하는 이유는 원 크기가 10이며 좌표 중앙에 원을 그리기 위함
                self.addEllipse((codx * 20) - 5, (cody * 15) - 5 , 10, 10, pen))
            if len(self.l) < 2: return
            r = self.l[-2].rect()
            last_ellipse_x, last_ellipse_y  = r.x(), r.y()
            print(last_ellipse_x, last_ellipse_y, codx * 20, cody * 15)
            self.addLine(r.x() +5, r.y()+5, codx*20, cody*15, pen)
    
    
    
    
        def draw_grid(self):
            width = Settings.NUM_BLOCKS_X.value * Settings.WIDTH.value
            height = Settings.NUM_BLOCKS_Y.value * Settings.HEIGHT.value
            self.setSceneRect(0, 0, width, height)
            self.setItemIndexMethod(QtWidgets.QGraphicsScene.NoIndex)
    
            pen = QPen(QColor(255,0,100), 1, Qt.SolidLine)
    
            for x in range(0,Settings.NUM_BLOCKS_X.value+1):
                xc = x * Settings.WIDTH.value
                self.lines.append(self.addLine(xc,0,xc,height,pen))
    
            for y in range(0,Settings.NUM_BLOCKS_Y.value+1):
                yc = y * Settings.HEIGHT.value
                self.lines.append(self.addLine(0,yc,width,yc,pen))
    
        def set_visible(self,visible=True):
            for line in self.lines:
                line.setVisible(visible)
    
        def delete_grid(self):
            for line in self.lines:
                self.removeItem(line)
            del self.lines[:]
    
        def set_opacity(self,opacity):
            for line in self.lines:
                line.setOpacity(opacity)
    
    
    class QV(QtWidgets.QGraphicsView):
    
        def __init__(self, *args, **kwargs):
            super().__init__(*args, **kwargs)
    
            self.view_menu = QMenu(self)
            self.create_actions()
            self.setMouseTracking(True)
    
    
        def create_actions(self):
            act = create_action(self.view_menu, "Zoom in",
                                slot=self.on_zoom_in,
                                shortcut=QKeySequence("+"), shortcut_context=Qt.WidgetShortcut)
            self.view_menu.addAction(act)
    
            act = create_action(self.view_menu, "Zoom out",
                                slot=self.on_zoom_out,
                                shortcut=QKeySequence("-"), shortcut_context=Qt.WidgetShortcut)
            self.view_menu.addAction(act)
    
            act = create_action(self.view_menu, "get coords",
                                slot=self.get_coords,
                                shortcut=QKeySequence(Qt.Key_Space),
                                shortcut_context=Qt.WidgetShortcut)
            self.view_menu.addAction(act)
            self.addActions(self.view_menu.actions())
    
        def get_coords(self):
            # SpaceBar를 누르면 누른 좌표를 출력
            if not self.scene():
                return
            sc = self.scene()
            ellipse = sc.l
            for e in ellipse:
                x, y = e.rect().x(), e.rect().y()
                print((x, y)),
    
        def on_zoom_in(self):
            if not self.scene():
                return
    
            self.scale(1.5, 1.5)
    
        def on_zoom_out(self):
            if not self.scene():
                return
    
            self.scale(1.0 / 1.5, 1.0 / 1.5)
    
        # def drawBackground(self, painter, rect):
        #     gr = rect.toRect()
        #     start_x = gr.left() + Settings.WIDTH - (gr.left() % Settings.WIDTH)
        #     start_y = gr.top() + Settings.HEIGHT - (gr.top() % Settings.HEIGHT)
        #     painter.save()
        #     painter.setPen(QtGui.QColor(60, 70, 80).lighter(90))
        #     painter.setOpacity(0.7)
        #
        #     for x in range(start_x, gr.right(), Settings.WIDTH):
        #         painter.drawLine(x, gr.top(), x, gr.bottom())
        #
        #     for y in range(start_y, gr.bottom(), Settings.HEIGHT):
        #         painter.drawLine(gr.left(), y, gr.right(), y)
        #
        #     painter.restore()
        #
        #     super().drawBackground(painter, rect)
    
    
    if __name__ == '__main__':
        app = QtWidgets.QApplication(sys.argv)
        a = QS()
        b = QV()
        b.setScene(a)
        # b.resize(800,600)
        b.show()
        sys.exit(app.exec_())

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/

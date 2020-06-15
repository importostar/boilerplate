---
title: game1
date: 2020-05-07
---
Example Python program game1.py
This program creates a PyQt GUI

## Modules

* import sys
* from PyQt5.QtCore import (
* from PyQt5.QtGui import (
* from PyQt5.QtWidgets import (

## Classes

* class Player(QGraphicsPixmapItem):
* class Bullet(QGraphicsPixmapItem):
* class Scene(QGraphicsScene):

## Methods

* def __init__(self, parent = None):
* def game_update(self, keys_pressed):
* def __init__(self, offset_x, offset_y, parent = None):
* def game_update(self, keys_pressed, player):
* def __init__(self, parent = None):
* def keyPressEvent(self, event):
* def keyReleaseEvent(self, event):
* def timerEvent(self, event):
* def game_update(self):

## Code

Example Python PyQt program :

    #
    # Simple start to a game in PyQt5
    #   move with arrow keys, spacebar to fire bullets
    # Used graphics from https://opengameart.org/content/space-shooter-redux
    # (reduced by 50%)
    # Got some hints from https://www.youtube.com/watch?v=8ntEQpg7gck series
    # and http://zetcode.com/gui/pyqt5/tetris/
    #
    import sys
    from PyQt5.QtCore import (
        Qt,
        QBasicTimer
    )
    from PyQt5.QtGui import (
        QBrush,
        QPixmap
    )
    from PyQt5.QtWidgets import (
        QApplication,
        QGraphicsItem,
        QGraphicsPixmapItem,
        QGraphicsRectItem,
        QGraphicsScene,
        QGraphicsView
    )
    
    SCREEN_WIDTH            = 800
    SCREEN_HEIGHT           = 600
    PLAYER_SPEED            = 3   # pix/frame
    PLAYER_BULLET_X_OFFSETS = [0,45]
    PLAYER_BULLET_Y         = 15
    BULLET_SPEED            = 10  # pix/frame
    BULLET_FRAMES           = 50
    FRAME_TIME_MS           = 16  # ms/frame
    
    class Player(QGraphicsPixmapItem):
        def __init__(self, parent = None):
            QGraphicsPixmapItem.__init__(self,parent)
            self.setPixmap(QPixmap("playerShip1_blue_sm.png"))
    
        def game_update(self, keys_pressed):
            dx = 0
            dy = 0
            if Qt.Key_Left in keys_pressed:
                dx -= PLAYER_SPEED
            if Qt.Key_Right in keys_pressed:
                dx += PLAYER_SPEED
            if Qt.Key_Up in keys_pressed:
                dy -= PLAYER_SPEED
            if Qt.Key_Down in keys_pressed:
                dy += PLAYER_SPEED
            self.setPos(self.x()+dx, self.y()+dy)
    
    class Bullet(QGraphicsPixmapItem):
        def __init__(self, offset_x, offset_y, parent = None):
            QGraphicsPixmapItem.__init__(self,parent)
            self.setPixmap(QPixmap("laserBlue07_sm.png"))
            self.offset_x = offset_x
            self.offset_y = offset_y
            self.active = False
            self.frames = 0
    
        def game_update(self, keys_pressed, player):
            if not self.active:
                if Qt.Key_Space in keys_pressed:
                    self.active = True
                    self.setPos(player.x()+self.offset_x,player.y()+self.offset_y)
                    self.frames = BULLET_FRAMES
            else:
                self.setPos(self.x(),self.y()-BULLET_SPEED)
                self.frames -= 1
                if self.frames <= 0:
                    self.active = False
                    self.setPos(SCREEN_WIDTH,SCREEN_HEIGHT)
    
    class Scene(QGraphicsScene):
        def __init__(self, parent = None):
            QGraphicsScene.__init__(self, parent)
    
            # hold the set of keys we're pressing
            self.keys_pressed = set()
    
            # use a timer to get 60Hz refresh (hopefully)
            self.timer = QBasicTimer()
            self.timer.start(FRAME_TIME_MS, self)
    
            bg = QGraphicsRectItem()
            bg.setRect(-1,-1,SCREEN_WIDTH+2,SCREEN_HEIGHT+2)
            bg.setBrush(QBrush(Qt.black))
            self.addItem(bg)
    
            self.player = Player()
            self.player.setPos((SCREEN_WIDTH-self.player.pixmap().width())/2,
                               (SCREEN_HEIGHT-self.player.pixmap().height())/2)
            self.bullets = [Bullet(PLAYER_BULLET_X_OFFSETS[0],PLAYER_BULLET_Y),
                            Bullet(PLAYER_BULLET_X_OFFSETS[1],PLAYER_BULLET_Y)]
            for b in self.bullets:
                b.setPos(SCREEN_WIDTH,SCREEN_HEIGHT)
                self.addItem(b)
            self.addItem(self.player)
    
            self.view = QGraphicsView(self)
            self.view.setHorizontalScrollBarPolicy(Qt.ScrollBarAlwaysOff)
            self.view.setVerticalScrollBarPolicy(Qt.ScrollBarAlwaysOff)
            self.view.show()
            self.view.setFixedSize(SCREEN_WIDTH,SCREEN_HEIGHT)
            self.setSceneRect(0,0,SCREEN_WIDTH,SCREEN_HEIGHT)
    
        def keyPressEvent(self, event):
            self.keys_pressed.add(event.key())
    
        def keyReleaseEvent(self, event):
            self.keys_pressed.remove(event.key())
    
        def timerEvent(self, event):
            self.game_update()
            self.update()
    
        def game_update(self):
            self.player.game_update(self.keys_pressed)
            for b in self.bullets:
                b.game_update(self.keys_pressed, self.player)
    
    if __name__ == '__main__':
        app = QApplication(sys.argv)
        scene = Scene()
        sys.exit(app.exec_())
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/

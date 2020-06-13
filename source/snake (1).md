---
title: snake (1)
date: 2020-05-07
---
Example Python program snake (1).py
This program creates a PyQt GUI

## Modules

* import sys, time
* import os
* from random import randrange
* from PyQt5.QtCore import *
* from PyQt5.QtWidgets import *
* from PyQt5.QtGui import *

## Classes

* class Snake(QMainWindow):
* class Board(QFrame):

## Methods

* def __init__(self):
* def initUI(self):
* def initMenu(self):
* def rules(self):
* def __init__(self, parent):
* def newGame(self):
* def getSpeed(self):
* def initSnake(self):
* def start(self):
* def pause(self):
* def paintEvent(self, event):
* def timerEvent(self, event):
* def keyPressEvent(self, event):
* def addFood(self, qp):
* def drawSnake(self, qp):
* def gameOver(self, event, qp):
* def direction(self, dir):
* def checkStatus(self, x, y):
* def main():

## Code

Example Python PyQt program :

    import sys, time
    import os
    from random import randrange
    
    from PyQt5.QtCore import *
    from PyQt5.QtWidgets import *
    from PyQt5.QtGui import *
    
    
    class Snake(QMainWindow):
        def __init__(self):
            super(Snake, self).__init__()
            self.initUI()
    
        def initUI(self):
            self.board = Board(self)
            self.setCentralWidget(self.board)
    
            self.statusbar = self.statusBar()
            self.board.scorestatus[str].connect(self.statusbar.showMessage)
    
            self.setFixedSize(600, 400)
    
            screen = QDesktopWidget().screenGeometry()
            size = self.geometry()
            self.move((screen.width() - size.width()) / 2,
                      (screen.height() - size.height()) / 2)
    
            self.initMenu()
            self.board.newGame()
    
            self.setWindowTitle('Snake')
            self.show()
    
        def initMenu(self):
            exitAction = QAction('&Exit', self)
            exitAction.setStatusTip('Exit')
            exitAction.triggered.connect(qApp.quit)
    
            rulesAction = QAction("&Rules", self, statusTip="Rules", triggered=self.rules)
    
            menubar = self.menuBar()
            fileMenu = menubar.addMenu('&File')
            fileMenu.addAction(exitAction)
            helpMenu = menubar.addMenu('&Help')
            helpMenu.addAction(rulesAction)
    
        def rules(self):
            QMessageBox.about(self, "Rules",
                              "The player controls the snake that moves around the framed board collecting food. " +
                              "Game ends if snake hits the walls or itself. The players' task is to grow the longest possible snake.<br><br>" +
                              "<b>Control</b>:<ul><li> ← ↑ → ↓ — control the movement of snake</li><li> P — pause/unpause the game</li><li> Space — start the new game</li></ul>")
    
    
    class Board(QFrame):
        scorestatus = pyqtSignal(str)
        highscore = 0
        cellsize = 20
    
        def __init__(self, parent):
            super(Board, self).__init__(parent)
            self.setFocusPolicy(Qt.StrongFocus)
    
        def newGame(self):
            self.getSpeed();
            self.initSnake()
    
            self.foodx = 0
            self.foody = 0
            self.lastKey = 'RIGHT'
    
            self.isOver = False
            self.isPaused = False
            self.foodPlaced = False
    
            self.timer = QBasicTimer()
    
            self.score = 0
            self.start()
    
        def getSpeed(self):
            timeOut, okPressed = QInputDialog.getInt(self, "Speed", "Snake speed: ", 2, 1, 5, 1,
                                                     Qt.WindowSystemMenuHint | Qt.WindowTitleHint)
            if okPressed:
                self.speed = 300 / timeOut
            else:
                self.speed = 150
    
        def initSnake(self):
            self.x = self.cellsize;
            self.y = self.cellsize * 3;
            self.snake = [[self.x, self.y], [0, self.y], [-self.x, self.y]]
    
        def start(self):
            self.isPaused = False
            self.timer.start(self.speed, self)
            self.update()
    
        def pause(self):
            self.isPaused = True
            self.timer.stop()
            self.update()
    
        # events
        def paintEvent(self, event):
            qp = QPainter()
            qp.begin(self)
            self.addFood(qp)
            self.drawSnake(qp)
            if self.isOver:
                self.gameOver(event, qp)
            qp.end()
    
        def timerEvent(self, event):
            if event.timerId() == self.timer.timerId():
                self.direction(self.lastKey)
                self.repaint()
            else:
                QFrame.timerEvent(self, event)
    
        def keyPressEvent(self, event):
            key = event.key()
    
            if not self.isPaused:
                if key == Qt.Key_Left and self.lastKey != 'RIGHT':
                    self.direction("LEFT")
                    self.lastKey = 'LEFT'
                elif key == Qt.Key_Right and self.lastKey != 'LEFT':
                    self.direction("RIGHT")
                    self.lastKey = 'RIGHT'
    
                elif key == Qt.Key_Up and self.lastKey != 'DOWN':
                    self.direction("UP")
                    self.lastKey = 'UP'
                elif key == Qt.Key_Down and self.lastKey != 'UP':
                    self.direction("DOWN")
                    self.lastKey = 'DOWN'
    
                elif key == Qt.Key_P:
                    self.pause()
    
            elif key == Qt.Key_P:
                self.start()
            elif key == Qt.Key_Space:
                self.newGame()
    
        def addFood(self, qp):
            if self.foodPlaced == False:
                size = self.geometry()
                self.foodx = randrange(int(size.width() / self.cellsize) - 2) * self.cellsize
                self.foody = randrange(2, int(size.height() / self.cellsize) - 2) * self.cellsize
                if not [self.foodx, self.foody] in self.snake:
                    self.foodPlaced = True;
    
            qp.setBrush(QColor(255, 222, 87))
            qp.drawRect(self.foodx, self.foody, self.cellsize, self.cellsize)
    
        def drawSnake(self, qp):
            qp.setBrush(QColor(69, 132, 182))
            for i in self.snake:
                qp.drawRect(i[0], i[1], self.cellsize, self.cellsize)
    
        def gameOver(self, event, qp):
            self.highscore = max(self.highscore, self.score)
            qp.setPen(QColor(100, 100, 100))
            qp.setFont(QFont('Decorative', 12))
            qp.drawText(event.rect(), Qt.AlignCenter, "GAME OVER \n press space to play again")
    
        def direction(self, dir):
            if (dir == "LEFT" and self.checkStatus(self.x - self.cellsize, self.y)):
                self.x -= self.cellsize
                self.repaint()
                self.snake.insert(0, [self.x, self.y])
            elif (dir == "RIGHT" and self.checkStatus(self.x + self.cellsize, self.y)):
                self.x += self.cellsize
                self.repaint()
                self.snake.insert(0, [self.x, self.y])
    
            elif (dir == "UP" and self.checkStatus(self.x, self.y - self.cellsize)):
                self.y -= self.cellsize
                self.repaint()
                self.snake.insert(0, [self.x, self.y])
            elif (dir == "DOWN" and self.checkStatus(self.x, self.y + self.cellsize)):
                self.y += self.cellsize
                self.repaint()
                self.snake.insert(0, [self.x, self.y])
    
        def checkStatus(self, x, y):
            size = self.geometry()
            # wall
            if y > size.height() - self.cellsize or x > size.width() - self.cellsize or x < 0 or y < 0:
                self.pause()
                self.isPaused = True
                self.isOver = True
                return False
            # suicide
            elif self.snake[0] in self.snake[1:len(self.snake)]:
                self.pause()
                self.isPaused = True
                self.isOver = True
                return False
            # food
            elif self.y == self.foody and self.x == self.foodx:
                self.foodPlaced = False
                self.score += 1
                return True
    
            self.scorestatus.emit("Score: " + str(self.score) + "\t\t\t Best score: " + str(self.highscore))
    
            self.snake.pop()
            return True
    
    
    def main():
        app = QApplication(sys.argv)
        scriptDir = os.path.dirname(os.path.realpath(__file__))
    
        game = Snake()
        sys.exit(app.exec_())
    
    
    if __name__ == '__main__':
        main()

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/

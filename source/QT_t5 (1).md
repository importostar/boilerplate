---
title: QT_t5 (1)
date: 2020-05-07
---
Example Python program QT_t5 (1).py
This program creates a PyQt GUI
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* from PyQt5 import QtCore, QtGui, QtWidgets
* from PyQt5.QtWidgets import QApplication, QWidget, QMainWindow, QLabel, QSlider, QInputDialog, QFileDialog, QPushButton, \
* from PyQt5.QtGui import QPainter, QColor, QPen, QIcon, QPixmap, QBrush, QImage
* from PyQt5.QtCore import Qt, QSize, QTimer  # pyqtSlot
* import os, sys, glob
* import numpy as np
* import cv2
* import sys

## Classes

* class PhotoViewer(QtWidgets.QGraphicsView):  # Grafikpanel, Klasse erbt Eigenschaften von QGraphicsView
* class Window(QtWidgets.QWidget):

## Methods

* def __init__(self, parent):
* def hasPhoto(self):
* def fitInView(self, scale=True):
* def setPhoto(self, pixmap=None):
* def wheelEvent(self, event):
* # def contextMenuEvent(self, event):
* def toggleDragMode(self):
* def mousePressEvent(self, event):
* def __init__(self):
* def keyPressEvent(self, event):
* # def convertVideo(self,frame)
* def loadVideo(self):
* def Select(self):
* def photoClicked(self, pos):
* def Area(self):
* def Scale(self):
* def Next(self):
* def Back(self):
* def StartF(self):
* def EndF(self):
* def Track(self):

## Code

Example Python PyQt program :

    from PyQt5 import QtCore, QtGui, QtWidgets
    
    from PyQt5.QtWidgets import QApplication, QWidget, QMainWindow, QLabel, QSlider, QInputDialog, QFileDialog, QPushButton, \
        QLineEdit
    from PyQt5.QtGui import QPainter, QColor, QPen, QIcon, QPixmap, QBrush, QImage
    from PyQt5.QtCore import Qt, QSize, QTimer  # pyqtSlot
    
    import os, sys, glob
    import numpy as np
    import cv2
    
    
    class PhotoViewer(QtWidgets.QGraphicsView):  # Grafikpanel, Klasse erbt Eigenschaften von QGraphicsView
        # create own signal
        photoClicked = QtCore.pyqtSignal(QtCore.QPoint)  # get x,y coordinates by clicking on the picture
    
        def __init__(self, parent):
            super(PhotoViewer, self).__init__(parent)  # accessing inherited methods
            self._zoom = 0
            self._empty = True
            self._scene = QtWidgets.QGraphicsScene(self)
            self._photo = QtWidgets.QGraphicsPixmapItem()
            self._scene.addItem(self._photo)
            self.setScene(self._scene)
    
            # fuer Mauskoordinaten
            self.setTransformationAnchor(QtWidgets.QGraphicsView.AnchorUnderMouse)
            self.setResizeAnchor(QtWidgets.QGraphicsView.AnchorUnderMouse)
            # keine nervigen Scrollbars
            self.setVerticalScrollBarPolicy(QtCore.Qt.ScrollBarAlwaysOff)
            self.setHorizontalScrollBarPolicy(QtCore.Qt.ScrollBarAlwaysOff)
            # Bild Hintergrundfarbe (schwarz)
            self.setBackgroundBrush(QtGui.QBrush(QtGui.QColor(0, 0, 0)))
            # Bildrahmen, options: WinPanel, StyledPanel
            self.setFrameShape(QtWidgets.QFrame.NoFrame)
    
        def hasPhoto(self):
            return not self._empty
    
        def fitInView(self, scale=True):
            rect = QtCore.QRectF(self._photo.pixmap().rect())
            if not rect.isNull():
                self.setSceneRect(rect)
                if self.hasPhoto():
                    unity = self.transform().mapRect(QtCore.QRectF(0, 0, 1, 1))
                    self.scale(1 / unity.width(), 1 / unity.height())
                    viewrect = self.viewport().rect()
                    scenerect = self.transform().mapRect(rect)
                    factor = min(viewrect.width() / scenerect.width(),
                                 viewrect.height() / scenerect.height())
                    self.scale(factor, factor)
                self._zoom = 0
    
        def setPhoto(self, pixmap=None):
            self._zoom = 0
            if pixmap and not pixmap.isNull():
                self._empty = False
                self.setDragMode(QtWidgets.QGraphicsView.ScrollHandDrag)
                self._photo.setPixmap(pixmap)
            else:
                self._empty = True
                self.setDragMode(QtWidgets.QGraphicsView.NoDrag)
                self._photo.setPixmap(QtGui.QPixmap())
            self.fitInView()
    
        # zoom
        def wheelEvent(self, event):
            if self.hasPhoto():
                if event.angleDelta().y() > 0:
                    factor = 1.25
                    self._zoom += 1
                else:
                    factor = 0.8
                    self._zoom -= 1
                if self._zoom > 0:
                    self.scale(factor, factor)
                elif self._zoom == 0:
                    self.fitInView()
                else:
                    self._zoom = 0
    
        # shortcuts
        # def contextMenuEvent(self, event):
        #	menu.addAction('Rotate CCW   r', partial(shufti.rotateImg, 1))
        #	menu.addAction('Spin CW    s', partial(shufti.rotateImg, -1))
        #	menu.addAction('Next image   SPACE', partial(shufti.dirBrowse, 1))
        #	menu.addAction('Previous image   BACKSPACE', partial(shufti.dirBrowse, -1))
        #	menu.addAction('Fit image   f', shufti.fitView)
        #	menu.addAction('Quit   q', shufti.close)
    
        # Verschiebe-Modus
        def toggleDragMode(self):
            if self.dragMode() == QtWidgets.QGraphicsView.ScrollHandDrag:
                self.setDragMode(QtWidgets.QGraphicsView.NoDrag)
            elif not self._photo.pixmap().isNull():
                self.setDragMode(QtWidgets.QGraphicsView.ScrollHandDrag)
    
        # x,y Pos des Mauszeigers
        def mousePressEvent(self, event):
            if self._photo.isUnderMouse():
                self.photoClicked.emit(QtCore.QPoint(event.pos()))
            super(PhotoViewer, self).mousePressEvent(event)
    
    
    class Window(QtWidgets.QWidget):
        # Oberflaeche
        def __init__(self):
            super(Window, self).__init__()
            self.viewer = PhotoViewer(self)
    
            # self.setFocusPolicy(Qt.StrongFocus)#try to handle up,down keys
    
            # Button 'Load video'
            self.btnLoad = QtWidgets.QToolButton(self)
            self.btnLoad.setText('Load video')
            self.btnLoad.clicked.connect(self.loadVideo)
    
            # Button Define area
            self.btnArea = QtWidgets.QToolButton(self)
            self.btnArea.setText('Select area')
            self.btnArea.clicked.connect(self.Area)
    
            # Button Set scaling
            self.btnScale = QtWidgets.QToolButton(self)
            self.btnScale.setText('Set scaling')
            self.btnScale.clicked.connect(self.Scale)
    
            # Edit current frame position
            self.editF = QtWidgets.QLineEdit(self)
    
            # Button Next picture
            self.btnNext = QtWidgets.QToolButton(self)
            self.btnNext.setText('>>>')
            self.btnNext.clicked.connect(self.Next)
    
            # Button picture Before
            self.btnBack = QtWidgets.QToolButton(self)
            self.btnBack.setText('<<<')
            self.btnBack.clicked.connect(self.Back)
    
            # Button Start (first frame)
            self.btnStartF = QtWidgets.QToolButton(self)
            self.btnStartF.setText('  [  ')
            self.btnStartF.clicked.connect(self.StartF)
    
            # Button End (last frame)
            self.btnEndF = QtWidgets.QToolButton(self)
            self.btnEndF.setText('  ]  ')
            self.btnEndF.clicked.connect(self.EndF)
    
            # Label StartF (first frame for calculation)
            self.lblStartF = QtWidgets.QLabel(self)
            self.lblStartF.setText('   0')
    
            # Label EndF (last frame for calculation)
            self.lblEndF = QtWidgets.QLabel(self)
            self.lblEndF.setText('')
    
            # Label LastF (number of last frame)
            self.lblLastF = QtWidgets.QLabel(self)
            self.lblLastF.setText('')
    
            # Button Select object (getting pixel info)
            self.btnSelect = QtWidgets.QToolButton(self)
            self.btnSelect.setText('Select object')
            self.btnSelect.clicked.connect(self.Select)
            # Get mouse position
            self.editPixInfo = QtWidgets.QLineEdit(self)
            # self.editPixInfo.setReadOnly(True)#nur Lesen erlaubt
            self.viewer.photoClicked.connect(self.photoClicked)
    
            # Button Tracking
            self.btnTrack = QtWidgets.QToolButton(self)
            self.btnTrack.setText('Tracking')
            self.btnTrack.clicked.connect(self.Track)
    
            # Arrange layout
            VBlayout = QtWidgets.QVBoxLayout(self)
            VBlayout.addWidget(self.viewer)
            HBlayout = QtWidgets.QHBoxLayout()
            HBlayout.setAlignment(QtCore.Qt.AlignLeft)
            HBlayout.addWidget(self.btnLoad)
            HBlayout.addWidget(self.btnArea)
            HBlayout.addWidget(self.btnScale)
            HBlayout.addWidget(self.lblStartF)
            HBlayout.addWidget(self.btnStartF)
            HBlayout.addWidget(self.btnBack)
            HBlayout.addWidget(self.editF)
            HBlayout.addWidget(self.lblLastF)
            HBlayout.addWidget(self.btnNext)
            HBlayout.addWidget(self.btnEndF)
            HBlayout.addWidget(self.lblEndF)
            HBlayout.addWidget(self.btnSelect)
            HBlayout.addWidget(self.btnTrack)
            HBlayout.addWidget(self.editPixInfo)
            VBlayout.addLayout(HBlayout)
    
        def keyPressEvent(self, event):
            key = event.key()
    
            if key == QtCore.Qt.Key_L:  # Bild laden
                print('Load picture')
                self.loadVideo()
            elif key == QtCore.Qt.Key_A:  # Define area
                self.Area()
            elif key == QtCore.Qt.Key_S:  # Set Scaling
                self.Scale()
            elif key == QtCore.Qt.Key_R:  # Bild rotieren
                print('Rotate!')
                self.viewer.rotate(90)
                self.viewer.fitInView()
            elif key == QtCore.Qt.Key_F:  # Bild im Fullview
                print('Full image view')
                self.viewer.fitInView()
            elif key == QtCore.Qt.Key_K:  # Frame vor
                self.Next()
            elif key == QtCore.Qt.Key_J:  # Frame zurueck
                self.Back()
            elif key == QtCore.Qt.Key_O:  # Select object
                self.Select()
            elif key == QtCore.Qt.Key_T:  # Tracking
                self.Track()
            elif key == QtCore.Qt.Key_Q:  # Programm schliessen
                self.close()
    
        # function for "convert/show video"
        # def convertVideo(self,frame)
        #	rgbImage = cv2.cvtColor(frame, cv2.COLOR_BGR2RGB)#convert to rgb
        #	qImg = QImage(rgbImage.data, rgbImage.shape[1], rgbImage.shape[0], QImage.Format_RGB888)#convert to Qt picture format
        #	self.viewer.setPhoto(QtGui.QPixmap(qImg)) #show picture, automatic scaling
        #	cv2.waitKey(1)#wait some time [ms] to show first picture immediately
    
        def loadVideo(self):
    
            print('load')
            video = QFileDialog.getOpenFileName(self, 'Single File', "./",
                                                "Video files (*.mov *.mp4 *.avi *.mkv)")  # select video, only video extensions allowed
            videoPath = video[0]  # store only videopath
            print('videoPath:', '\n', videoPath, '\n')
    
            # -------------- Video laden ----------------- #(eigener thread, damit direkt Kalibrierung moeglich?
            cap = cv2.VideoCapture(videoPath)  # Pass absolute address of video file
            check, frame = cap.read()  # Grab current frame, check: frame was read succesfully?
            counter = 0  # counting frames
            global frame_end
            frame_end = counter
            global frame_list
            frame_list = []  # store all frames in list
            # If reached the end of the video then we got False value of check!
            while (check == True):
                # show first picture immediately
                if counter == 0:
                    rgbImage = cv2.cvtColor(frame, cv2.COLOR_BGR2RGB)  # convert to rgb
                    qImg = QImage(rgbImage.data, rgbImage.shape[1], rgbImage.shape[0],
                                  QImage.Format_RGB888)  # convert to Qt picture format
                    self.viewer.setPhoto(QtGui.QPixmap(qImg))  # show picture, automatic scaling
                    cv2.waitKey(1)  # wait some time [ms] to show first picture immediately
                    print('Printed first frame')
                    global frame_nr  # aktuelle Frame-Nummer
                    frame_nr = 0
                print(counter + 1)
                frame_list.append(frame)  # store frame in list
                check, frame = cap.read()
                counter += 1
    
            if counter > 0:
                frame_end = counter - 1
            print('Letztes Frame:', frame_end + 1)
            cap.release()  # release cap, object clean
            self.editF.setText(str(frame_nr + 1))
            self.lblLastF.setText('/ ' + str(frame_end + 1))
    
        def Select(self):
            self.viewer.toggleDragMode()
            # bbox = cv2.selectROI(frame_list[frame_nr], False)
            print('Select Object')
    
        def photoClicked(self, pos):
            if self.viewer.dragMode() == QtWidgets.QGraphicsView.NoDrag:
                self.editPixInfo.setText('%d, %d' % (pos.x(), pos.y()))
    
        def Area(self):
            print('Select Area')
    
        def Scale(self):
            print('Define length between two points')
    
        def Next(self):
            global frame_list
            global frame_nr
            global frame_end
            if frame_nr < frame_end:
                frame_nr += 1
                # show frame
                rgbImage = cv2.cvtColor(frame_list[frame_nr], cv2.COLOR_BGR2RGB)  # convert to rgb
                qImg = QImage(rgbImage.data, rgbImage.shape[1], rgbImage.shape[0],
                              QImage.Format_RGB888)  # convert to Qt picture format
                self.viewer.setPhoto(QtGui.QPixmap(qImg))  # show picture, automatic scaling
            cv2.waitKey(1)  # wait some time [ms] to show first picture immediately
            print(frame_nr + 1)
            self.editF.setText(str(frame_nr + 1))
    
        def Back(self):
            global frame_list
            global frame_nr
            if frame_nr > 0:
                frame_nr -= 1
                # show frame
                rgbImage = cv2.cvtColor(frame_list[frame_nr], cv2.COLOR_BGR2RGB)  # convert to rgb
                qImg = QImage(rgbImage.data, rgbImage.shape[1], rgbImage.shape[0],
                              QImage.Format_RGB888)  # convert to Qt picture format
                self.viewer.setPhoto(QtGui.QPixmap(qImg))  # show picture, automatic scaling
                cv2.waitKey(1)  # wait some time [ms] to show first picture immediately
            print(frame_nr + 1)
            self.editF.setText(str(frame_nr + 1))
    
        def StartF(self):
            print('First Frame')
    
        def EndF(self):
            print('Last frame')
    
        def Track(self):
            print('Tracking...')
    
    
    if __name__ == '__main__':
        import sys
    
        app = QtWidgets.QApplication(sys.argv)
        window = Window()
        window.setGeometry(100, 30, 960, 576)  # HD1080=1920x1080, (1280x720)
        window.show()
        sys.exit(app.exec_())
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/

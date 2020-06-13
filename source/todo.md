---
title: todo
date: 2020-05-07
---
Example Python program todo.py

## Modules

* from PyQt5.QtCore import QThread
* from cv2 import VideoCapture, CAP_PROP_FRAME_COUNT, CAP_PROP_FPS, CAP_PROP_POS_MSEC, CAP_PROP_FRAME_HEIGHT, \

## Classes

* class CV2Player(QThread):

## Methods

* def __init__(self, parent=None):
* def load_video(self, filepath):
* def play(self):
* def stop(self):
* def run(self):

## Code

Example Python PyQt program :

    from PyQt5.QtCore import QThread
    from cv2 import VideoCapture, CAP_PROP_FRAME_COUNT, CAP_PROP_FPS, CAP_PROP_POS_MSEC, CAP_PROP_FRAME_HEIGHT, \
        CAP_PROP_FRAME_WIDTH
    
    
    # in OpenCV version 4.8 (used by gi?), VideoCapture.get() can't use CAP_PROP_FPS etc
    
    # CAP_PROP_POS_MSEC = 0
    # CAP_PROP_FPS = 5
    # CAP_PROP_FRAME_COUNT = 7
    
    
    class CV2Player(QThread):
    
        def __init__(self, parent=None):
            super(CV2Player, self).__init__(parent)
            self.video = VideoCapture()
            self.stop = True
            self.mutex = None
            self.reset_frame_props()
            self.frame_height = 0
            self.frame_width = 0
            self.frame_count = 0
            self.fps = -1
            self.frame_delay = 0
    
        def load_video(self, filepath):
            self.video.open(filepath)
            if self.video.isOpened():
                self.frame_count = int(self.video.get(CAP_PROP_FRAME_COUNT))
                self.fps = int(self.video.get(CAP_PROP_FPS))
                self.frame_delay = self.video.get(CAP_PROP_POS_MSEC)
                self.frame_height = self.video.get(CAP_PROP_FRAME_HEIGHT)
                self.frame_width = self.video.get(CAP_PROP_FRAME_WIDTH)
                return True
            return False
    
        def play(self):
            if not self.isRunning():
                if self.isStopped():
                    self.stop = False
                self.start(QThread.NormalPriority)
    
        def stop(self):
            self.stop = True
    
        def run(self):
            if self.frame_rate <= 0:
                return
            while not self.stop:
                success, frame = self.video.read()
                if not success:
                    self.stop = True
                    return
    
    
    
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/

---
title: video_player
date: 2020-05-07
---
Example Python program video_player.py

## Modules

* import cv2

## Classes

* class VideoPlayer():

## Methods

* def __init__(self):
* def load_video(self, in_path, out_path):
* def get_next_frame(self):
* # def get_next_frame(self, id):
* def write_next_frame(self, frame):
* def release(self):

## Code

Python example

    import cv2
    
    
    class VideoPlayer():
        def __init__(self):
            self.in_cap = None
            self.out_cap = None
            self.fps = 0
            self.frame_h = 0
            self.frame_w = 0
            self.num_frame = 0
            self.frame_id = 0
    
        def load_video(self, in_path, out_path):
            self.in_cap = cv2.VideoCapture(in_path)
            self.fps = self.in_cap.get(cv2.CAP_PROP_FPS)
            self.frame_w = int(self.in_cap.get(3))
            self.frame_h = int(self.in_cap.get(4))
            self.num_frame = int(self.in_cap.get(cv2.CAP_PROP_FRAME_COUNT))
            self.out_cap = cv2.VideoWriter(out_path,  cv2.VideoWriter_fourcc(
                'X', 'V', 'I', 'D'), self.fps, (self.frame_w, self.frame_h))
    
        def get_next_frame(self):
            retval, img = self.in_cap.read()
            return retval, img
    
        # -----Bug
        # in_cap.set(1, id) + in_cap.read() is very slow
        # def get_next_frame(self, id):
        #     self.in_cap.set(1, id)
        #     ret, img = self.in_cap.read()
        #     return img
        # -----
    
        def write_next_frame(self, frame):
            self.out_cap.write(frame)
    
        def release(self):
            self.in_cap.release()
            self.out_cap.release()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

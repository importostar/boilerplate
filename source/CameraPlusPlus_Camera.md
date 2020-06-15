---
title: CameraPlusPlus_Camera
date: 2020-05-07
---
Example Python program CameraPlusPlus_Camera.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import cv2
* import time
* from PyQt5.QtCore import QThread

## Classes

* class UsbCamera(QThread):

## Methods

* def __init__(self):
* def run(self):
* def setPara(self, wind_name, camera_idxs):
* def pauseFlag(self):
* def exitFlag(self):

## Code

Example Python PyQt program :

    # -*- coding: utf-8 -*-
    
    import cv2
    import time
    from PyQt5.QtCore import QThread
    
    
    class UsbCamera(QThread):
        exit_flag = False
        pause_flag = False
        window_name = ""
        camera_idx = 0
    
        def __init__(self):
            super().__init__()
    
        def run(self):
            # cv2.namedWindow(self.window_name)
            # 视频来源，可以来自一段已存好的视频，也可以直接来自USB摄像头
            cap = cv2.VideoCapture(self.camera_idx)
            fourcc = cv2.VideoWriter_fourcc(*'XVID')
            self.exit_flag = False
            while True:
                if self.exit_flag:
                    break
                if self.pause_flag:
                    time.sleep(0.1)
                    continue
                now = time.strftime("%Y-%m-%d-%H_%M_%S", time.localtime(time.time()))
                video_name = now + "_camera_" + str(self.camera_idx) + ".avi"
                out = cv2.VideoWriter(video_name, fourcc, 12.0, (640, 480))
                # 告诉OpenCV使用人脸识别分类器
                classfier = cv2.CascadeClassifier(cv2.data.haarcascades + "haarcascade_frontalface_alt2.xml")
                # 识别出人脸后要画的边框的颜色，RGB格式
                color = (0, 255, 0)
                while cap.isOpened():
                    if self.pause_flag:
                        break
                    ok, frame = cap.read()  # 读取一帧数据
                    if not ok:
                        print("VideoCapture Error")
                        break
                    # 将当前帧转换成灰度图像
                    grey = cv2.cvtColor(frame, cv2.COLOR_BGR2GRAY)
    
                    # 人脸检测，1.2和2分别为图片缩放比例和需要检测的有效点数
                    faceRects = classfier.detectMultiScale(grey, scaleFactor=1.2, minNeighbors=3, minSize=(32, 32))
                    if len(faceRects) > 0:  # 大于0则检测到人脸
                        for faceRect in faceRects:  # 单独框出每一张人脸
                            x, y, w, h = faceRect
                            cv2.rectangle(frame, (x - 10, y - 10), (x + w + 10, y + h + 10), color, 2)
    
                    out.write(frame)
                    # 显示图像
                    # cv2.imshow(self.window_name, frame)
                    # c = cv2.waitKey(1)
                    # time.sleep(20)
                    # if c & 0xFF == ord('q'):
                    #   break
    
                # 释放摄像头并销毁所有窗口
                cap.release()
                out.release()
                cv2.destroyAllWindows()
    
        def setPara(self, wind_name, camera_idxs):
            self.window_name = wind_name
            self.camera_idx = camera_idxs
    
        def pauseFlag(self):
            self.pause_flag = True
    
        def exitFlag(self):
            if self.exit_flag:
                self.exit_flag = False
            else:
                self.exit_flag = True
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/
- Tutorial: https://pythonprogramminglanguage.com/

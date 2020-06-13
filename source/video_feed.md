---
title: video_feed
date: 2020-05-07
---
Example Python program video_feed.py

## Modules

* import tkinter
* import cv2
* import PIL.Image, PIL.ImageTk
* import time
* import numpy as np
* import string
* import random

## Classes

* class App:
* class MyVideoCapture:

## Methods

* def __init__(self, window, window_title, video_source=0):
* def mouse1_event(self, event):
* def mouse2_event(self, event):
* def clear_all_lines(self):
* def clear_current_lines(self):
* def file_id_gen(self, size=6, chars=string.ascii_uppercase + string.digits):
* def snapshot(self):
* def draw_lines(self, frame):
* def show_areas(self, frame):
* def crop_image(self):
* def update(self):
* def __init__(self, video_source=0):
* def get_frame(self):
* def __del__(self):

## Code

Python tkinter example

    import tkinter
    import cv2
    import PIL.Image, PIL.ImageTk
    import time
    import numpy as np
    import string
    import random
    
    
    class App:
        def __init__(self, window, window_title, video_source=0):
            self.window = window
            self.window.title(window_title)
            self.video_source = video_source
            # open video source (by default this will try to open the computer webcam)
            self.vid = MyVideoCapture(self.video_source)
    
            self.bet_coords = []
            self.bet_coords_tmp = []
            self.frame = ''
    
            # Create a canvas that can fit the above video source size
            self.canvas = tkinter.Canvas(window, width=1440, height=900)
            self.canvas.bind('<Button-1>', self.mouse1_event)
            self.canvas.bind('<Button-3>', self.mouse2_event)
            self.canvas.pack()
    
            self.button_area = tkinter.Canvas(window)
            self.button_area.pack()
    
            # Button that lets the user take a snapshot
            self.btn_snapshot = tkinter.Button(self.button_area, text="Snapshot", width=50, command=self.snapshot)
            self.btn_snapshot.pack(anchor=tkinter.CENTER, expand=True)
    
            # Buttons to clear lines
            self.btn_clear_all_lines = tkinter.Button(self.button_area, text="Clear all areas", width=50,
                                                      command=self.clear_all_lines)
            self.btn_clear_all_lines.pack(anchor=tkinter.CENTER, expand=True)
    
            self.btn_clear_current_lines = tkinter.Button(self.button_area, text="Clear current area", width=50,
                                                          command=self.clear_current_lines)
            self.btn_clear_current_lines.pack(anchor=tkinter.CENTER, expand=True)
    
            # Button that lets user take cropped snapshots
            self.btn_cropped = tkinter.Button(self.button_area, text="Crop images", width=50, command=self.crop_image)
            self.btn_cropped.pack(anchor=tkinter.CENTER, expand=True)
    
            # After it is called once, the update method will be automatically called every delay milliseconds
            self.delay = 1
            self.update()
    
            self.window.mainloop()
    
        # left mouse button to record the x, y axis of the click
        def mouse1_event(self, event):
            self.bet_coords_tmp.append([event.x, event.y])
    
        # right mouse button to store each area
        def mouse2_event(self, event):
            self.bet_coords.append(self.bet_coords_tmp.copy())
            self.bet_coords_tmp.clear()
    
        def clear_all_lines(self):
            self.bet_coords.clear()
    
        def clear_current_lines(self):
            self.bet_coords_tmp.clear()
    
        def file_id_gen(self, size=6, chars=string.ascii_uppercase + string.digits):
            return ''.join(random.choice(chars) for _ in range(size))
    
        def snapshot(self):
            # Get a frame from the video source
            ret, self.frame = self.vid.get_frame()
            if ret:
                cv2.imwrite("./snapshots/frame-" + time.strftime("%d-%m-%Y-%H-%M-%S") + self.file_id_gen() +
                            ".jpg", cv2.cvtColor(self.frame, cv2.COLOR_BGR2RGB))
    
        def draw_lines(self, frame):
            # draw polygon from each click
            cv2.polylines(frame, [np.array([self.bet_coords_tmp])], 1, (0, 0, 0), 2)
            return frame
    
        def show_areas(self, frame):
            # draw all areas that have been stored
            for i in range(len(self.bet_coords)):
                cv2.polylines(frame, [np.array([self.bet_coords[i]])], 1, (0, 0, 0), 2)
            return frame
    
        def crop_image(self):
            self.bet_coords_array = np.array(self.bet_coords)
            for i in self.bet_coords_array:
                i = np.array(i)
                rect = cv2.boundingRect(i)
                x, y, w, h = rect
                cropped = self.frame[y:y + h, x:x + w]
                pts = np.array(i) - np.array(i).min(axis=0)
                ctr = np.array(pts).reshape((-1, 1, 2)).astype(np.int32)
                mask = np.zeros(cropped.shape[:2], np.uint8)
                cv2.drawContours(mask, [ctr], -1, (255, 255, 255), -1, cv2.LINE_AA)
                dst = cv2.bitwise_and(cropped, cropped, mask=mask)
                crp = cv2.cvtColor(dst, cv2.COLOR_BGR2RGB)
                np.array(crp)
                cv2.imwrite('./cropped/frame-' + time.strftime("%d-%m-%Y-%H-%M-%S") + self.file_id_gen() + ".jpg", crp)
    
        def update(self):
            # Get a frame from the video source
            ret, self.frame = self.vid.get_frame()
    
            if ret:
                if len(self.bet_coords_tmp) > 0:
                    self.frame = self.draw_lines(self.frame)
                if len(self.bet_coords) > 0:
                    self.frame = self.show_areas(self.frame)
                self.photo = PIL.ImageTk.PhotoImage(image=PIL.Image.fromarray(self.frame))
                self.canvas.create_image(0, 0, image=self.photo, anchor=tkinter.NW)
    
            self.window.after(self.delay, self.update)
    
    
    class MyVideoCapture:
        def __init__(self, video_source=0):
            # Open the video source
            self.vid = cv2.VideoCapture(video_source)
            if not self.vid.isOpened():
                raise ValueError("Unable to open video source", video_source)
    
            # Get video source width and height
            self.width = self.vid.set(cv2.CAP_PROP_FRAME_WIDTH, 1440)
            self.height = self.vid.set(cv2.CAP_PROP_FRAME_HEIGHT, 900)
    
            #self.width = self.vid.get(cv2.CAP_PROP_FRAME_WIDTH)
            #self.height = self.vid.get(cv2.CAP_PROP_FRAME_HEIGHT)
    
        def get_frame(self):
            if self.vid.isOpened():
                ret, frame = self.vid.read()
                # draw line over the frame
    
                if ret:
                    # Return a boolean success flag and the current frame converted to RGB
                    return (ret, cv2.cvtColor(frame, cv2.COLOR_BGR2RGB))
    
                else:
                    return (ret, None)
    
        # Release the video source when the object is destroyed
        def __del__(self):
            if self.vid.isOpened():
                self.vid.release()
    
    
    # Create a window and pass it to the Application object
    App(tkinter.Tk(), "Tkinter and OpenCV")
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

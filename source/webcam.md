---
title: webcam
date: 2020-05-07
---
Example Python program webcam.py

## Modules

* import tkinter
* import cv2
* from PIL import Image
* from PIL import ImageTk

## Methods

* def videoLoop():

## Code

Python tkinter example

    import tkinter
    import cv2
    from PIL import Image
    from PIL import ImageTk
    
    root = tkinter.Tk()
    
    # The frame is used for layout management
    imageFrame = tkinter.Frame(root, width=800, height=600)
    imageFrame.grid(row=0, column=0, padx=10, pady=2)
    
    # Added a label to the frame to display the image
    panel = tkinter.Label(imageFrame)
    panel.grid(row=0, column=0)
    
    cap = cv2.VideoCapture(0)
    # Check if the webcam is opened correctly
    if not cap.isOpened():
        raise IOError("Cannot open webcam")
    
    
    def videoLoop():
        ret, frame = cap.read()
        cv2image = cv2.cvtColor(frame, cv2.COLOR_BGR2RGBA)
    
        img = Image.fromarray(cv2image).resize((800, 600))
        imgtk = ImageTk.PhotoImage(image=img)
        panel.imgtk = imgtk
        panel.configure(image=imgtk)
        panel.after(10, videoLoop)
    
    videoLoop()
    root.mainloop()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

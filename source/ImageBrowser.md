---
title: ImageBrowser
date: 2020-05-07
---
Example Python program ImageBrowser.py
For Python version 2.x.
To test your Python version use:

    python --version

## Modules

* import Tkinter as tk
* from PIL import Image, ImageTk
* import glob, os

## Methods

* def SetImg(newPath):
* def ShiftCurImg(amount):
* def key(event):

## Code

Python tkinter example

    
    import Tkinter as tk
    from PIL import Image, ImageTk
    import glob, os
    
    
    # image types we're gonna check for
    valid_images = [".jpg",".gif",".png",".tga",".jpeg",".bmp",".webm"]
    
    imageList = []
    
    curImg = 0
    
    #find images in directory
    for x in valid_images:
        for file in glob.glob("*" + x):
            imageList.append(file)
    
    print(imageList)
    
    print len(imageList)
    
    #This creates the main window of an application
    window = tk.Tk()
    window.title("Join")
    
    window.configure(background='grey')
    
    
    path = "sample.png"
    img = ImageTk.PhotoImage(Image.open(path))
    window.geometry(str(img.width()) + "x" + str(img.height()))
    #Creates a Tkinter-compatible photo image, which can be used everywhere Tkinter expects an image object.
    
    #The Label widget is a standard Tkinter widget used to display a text or image on the screen.
    panel = tk.Label(window, image = img)
    
    #The Pack geometry manager packs widgets in rows or columns.
    panel.pack(side = "bottom", fill = "both", expand = "yes")
    
    def SetImg(newPath):
        global img
        global panel
        global window
        img = ImageTk.PhotoImage(Image.open(newPath))
        panel.configure(image=img)
        window.geometry(str(img.width()) + "x" + str(img.height()))
        window.update()
    
    def ShiftCurImg(amount):
        global curImg
        curImg = (curImg + amount) % (len(imageList))
        print 'Attempting to access image index: ' + str(curImg)
        SetImg(imageList[curImg])
    
    #SetImg(path)
    
    #create keypress event method.
    def key(event):
        if event.keysym == 'Left':
            ShiftCurImg(-1)
        elif event.keysym == 'Right':
            ShiftCurImg(1)
    
    #Start the GUI
    
    window.bind_all('<Key>', key)
    window.mainloop()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

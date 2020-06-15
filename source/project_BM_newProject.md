---
title: project_BM_newProject
date: 2020-05-07
---
Example Python program project_BM_newProject.py

## Modules

* import os
* from tkinter import *   ## notice lowercase 't' in tkinter here
* import picamera
* #import getTime
* from pathlib import Path
* import time
* from time import sleep
* from PIL import Image
* import matplotlib.pyplot as plt
* import matplotlib.image as mpimg
* import sys

## Methods

* def form_new_project():
* def goBack():
* def cam():
* def BtnStartCmd():

## Code

Python tkinter example

    import os
    from tkinter import *   ## notice lowercase 't' in tkinter here
    import picamera
    #import getTime
    from pathlib import Path
    import time
    from time import sleep
    from PIL import Image
    import matplotlib.pyplot as plt
    import matplotlib.image as mpimg
    import sys
    
    def form_new_project():
        timeNow = time.strftime("%H") + "." + time.strftime("%M") + "." + time.strftime("%S")
        date = time.strftime("%d.%m.%y")
        rootPath = rootPath = str(Path.home()) + str("/BM")
        ImageRoot = rootPath + "/" + date + "/" + timeNow + ".png"
        mainView = Tk()
    
        def goBack():
            sys.exit(0)
        ImageRoot = str("")
        def cam():
            pass
        #Path for the project lib
    
    
        #Form settings
        screen_width =  mainView.winfo_screenwidth()
        screen_height = mainView.winfo_screenheight()
        screen_resolution = str(screen_width) + 'x' + str(screen_height)
    
        mainView.geometry(screen_resolution)
        mainView.attributes("-fullscreen",True)
    
        mainView.title("Start a new project ")
    
        #Objects (widgets)
    
    
        exitBtn = Button(mainView, text="exit", command=exit, bg='red')
        exitBtn.pack(anchor='n', side=RIGHT)
    
        backBtn = Button(mainView, text="Back", command=goBack, bg='Blue')
        backBtn.pack(anchor='n', side=RIGHT)
    
    
        Left_Frame = Frame(mainView, bg="red", height= 480, width =500)
        Left_Frame.place(relx=.0, rely=.5, anchor="center")
    
        RightFrame = Frame(mainView,bg="red",height=400,width=400)
        RightFrame.place(relx=0.9,rely=.5, anchor="e")
    
        info_text = "Here you can take a snap shoot of your  BM \n Les's start by clicking the button 'new scan' "
    
        info_lable = Label(Left_Frame, text=info_text, fg='White', bg='Black' )
        info_lable.place(relx=.5, rely=.1, anchor="w")
    
    
    
        def BtnStartCmd():
            StartButton.config(text="")
    
            if not os.path.exists(rootPath + "/" + date ):
                os.makedirs(rootPath + "/" + date)
            camera = picamera.PiCamera()
            camera.brightness = 60
            camera.start_preview()
            sleep(5)
            camera.stop_preview()
            sleep(0.1)
            img = rootPath + "/" + date + "/" + timeNow + ".png"
            camera.capture(img)
            Image.open(img).show()
            showImage = mpimg.imread(img)
            imgplot = plt.imshow(showImage)
            plt.show()
    
    
        StartButton = Button(Left_Frame, text="Click here to start a new scan",command=BtnStartCmd)
        StartButton.place(relx=.625, rely=.5, anchor="w")
    
    
    
        mainView.mainloop()
    
    
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

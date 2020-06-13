---
title: iflat
date: 2020-05-07
---
Example Python program iflat.py

## Modules

* import cv2
* import numpy as np
* import Tkinter
* import tkMessageBox
* from tkFileDialog import askopenfilename

## Classes

* class TkApp(Tkinter.Tk):

## Methods

* def limit(x, mini, maxi):
* def iflat(img, calib):
* def __init__(self, parent):
* def select_calib(self):
* def select_target(self):
* def launch(self):
* def main():

## Code

Python tkinter example

    #!/usr/bin/python2
    
    import cv2
    import numpy as np
    import Tkinter
    import tkMessageBox
    from tkFileDialog import askopenfilename
    
    HELP = """
    This script have been made to counter brightness irregularity
    Select calibration image (blank image)
    and target image
    
    Both images must have been taken under the exact same light
    
    (see example in test folder)
    
    result will saved under result.png
    """
    
    def limit(x, mini, maxi):
        if (x < mini):
            x = mini
        elif (x > maxi):
            x = maxi
        elif (x != x):
            x = 0
        return (x)
    
    def iflat(img, calib):
        calib = cv2.GaussianBlur(calib, (7,7), 0)
        av = np.average(calib)
        height, width = calib.shape
        for col in range(width):
            for row in range(height):
                coef = calib.item(row, col) / av
                if (coef == 0):
                    coef = 1
                pix = img.item(row, col) / coef
                pix = limit(pix, 0, 255)
                img.itemset(row, col, pix)
        return (img)
    
    class TkApp(Tkinter.Tk):
        def __init__(self, parent):
            Tkinter.Tk.__init__(self, parent)
            self.calib_file = ""
            self.target_file = ""
            self.parent = parent
            label = Tkinter.Label(self, text=HELP)
            label.pack(side=Tkinter.TOP)
            b1 = Tkinter.Button(self, text="Select calib image", command=self.select_calib)
            b1.pack(side=Tkinter.LEFT)
            b2 = Tkinter.Button(self, text="Select target image", command=self.select_target)
            b2.pack(side=Tkinter.RIGHT)
            b3 = Tkinter.Button(self, text="Launch", command=self.launch)
            b3.pack(side=Tkinter.BOTTOM)
        
        def select_calib(self):
            self.calib_file = askopenfilename()
        
        def select_target(self):
            self.target_file = askopenfilename()
        
        def launch(self):
            if (not self.calib_file or not self.calib_file):
                tkMessageBox.showerror("Error", "Select target and calibration image")
                return
            self.quit()
            calib = cv2.imread(self.calib_file, cv2.CV_LOAD_IMAGE_GRAYSCALE)
            img = cv2.imread(self.target_file, cv2.CV_LOAD_IMAGE_GRAYSCALE)
            if (img.size != calib.size):
                tkMessageBox.showerror("Error", "Both images must be same size")
            result = iflat(img, calib)
            cv2.namedWindow('image',cv2.WINDOW_NORMAL)
            cv2.resizeWindow('image', 800, 800)
            cv2.imshow("image", result)
            cv2.imwrite("result.png", result);
            cv2.waitKey(0)
    
    def main():
        app = TkApp(None)
        app.title("iflat script")
        app.geometry("400x200")
        app.mainloop()
        '''
        calib = cv2.imread("test/flat.bmp",
                            cv2.CV_LOAD_IMAGE_GRAYSCALE)
        img = cv2.imread("test/usaf.bmp",
                            cv2.CV_LOAD_IMAGE_GRAYSCALE)
        result = iflat(img, calib)
        cv2.namedWindow('image',cv2.WINDOW_NORMAL)
        cv2.resizeWindow('image', 800, 800)
        cv2.imshow("image", result)
        cv2.imwrite("result.png", result);
        cv2.waitKey(0)
        '''
    
    
    if (__name__=="__main__"):
        main()
    
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

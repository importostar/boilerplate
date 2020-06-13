---
title: project_BM_imageProcessing
date: 2020-05-07
---
Example Python program project_BM_imageProcessing.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import cv2
* import os
* import shutil
* #from PIL import Image
* import numpy as np

## Methods

* def task1():

## Code

Python example

    '''
    Figure 6. (a) Original skin lesion image; (b) the image filtered by Gaussian filter; (c)
    the image filtered by bilateral filter.
    '''
    
    import cv2
    import os
    import shutil
    #from PIL import Image
    import numpy as np
    
    desktopPath = os.path.join(os.path.join(os.environ['USERPROFILE']), 'Desktop')
    filePath = desktopPath + str("\BM.png")
    print("first path" + desktopPath  + "\nsecound path " +filePath)
    endPath = desktopPath + str("/image_gray.png")
    
    
    '''
    now we will take the image and create a duplication of himself 
    '''
    def task1():
        shutil.copy(filePath, endPath)
    
    if not os.path.isfile(endPath):
        task1()
    else:
        os.remove(endPath)
        task1()
    
    
    
    
    image = cv2.imread(filePath)
    gray_image = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)
    cv2.imwrite(desktopPath + str("\gray_image_dup.png") , gray_image )
    
    #The idea is to get the color (0-255)
    #px = gray_image[12,100]
    #print(px)
    
    
    #for loop to get the image brg value
    px = None
    counter_gray = counter_other = 0
    '''
    
    for y in range(0,599):
        for x in range(0,999):
            px = gray_image[y][x]
            if px==136:
                counter_gray = counter_gray + 1
            else:
                counter_other = counter_other + 1
    
    
    print("We have " + str(counter_gray)  + " gray pixels and " + str(counter_other) + " blue pixels")
    
    #Convert the copy of the image to gray Scale
    '''
    
    
    
    #this array helps up to orgenize the pixels to groups
    #in place 0 we have 0 til 15
    #In place 1 we have 16 til 32
    #in place 2 we have 33 til 39
    #in place 3 we have 40 til 56
    #in place 4 we have 57 til 64
    #""
    
    colorArray = [0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0]
    
    #here start to seperate the pixels to groups
    print("\n\n\n")
    for y in range(0,165):
        for x in range(0,165):
            px = gray_image[y][x]
            # add 1 to the color array in the first spot
            if  px >= 0 and px <16:
                colorArray[0] += 1
            elif  px >= 16 and px <32:
                colorArray[1] +=1
            elif px>=32 and px < 48:
                colorArray[2] += 1
            elif px >= 48 and px < 64:
                colorArray[3] += 1
            elif  px >= 64 and px <80:
                colorArray[4] +=1
            elif px>=80 and px < 96:
                colorArray[5] += 1
            elif px >= 96 and px < 112:
                colorArray[6] += 1
            elif  px >= 112 and px <128:
                colorArray[7] +=1
            elif px>=128 and px < 144:
                colorArray[8] += 1
            elif px >= 144 and px < 160:
                colorArray[9] += 1
            elif px >= 160 and px < 176:
                colorArray[10] += 1
            elif  px >= 176 and px <192:
                colorArray[11] +=1
            elif px>=192 and px < 208:
                colorArray[12] += 1
            elif px >= 208 and px < 224:
                colorArray[13] += 1
            elif  px >= 224 and px <240:
                colorArray[14] +=1
            elif px>=240 and px < 256:
                colorArray[15] += 1
    
    print(colorArray[0])
    print(colorArray[1])
    print(colorArray[2])
    print(colorArray[3])
    print(colorArray[4])
    print(colorArray[5])
    print(colorArray[6])
    print(colorArray[7])
    print(colorArray[8])
    print(colorArray[9])
    print(colorArray[10])
    print(colorArray[11])
    print(colorArray[12])
    print(colorArray[13])
    print(colorArray[14])
    print(colorArray[15])
    
    
    
    
    
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

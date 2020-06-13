---
title: dither
date: 2020-05-07
---
Example Python program dither.py

## Modules

* import Tkinter
* import Image, ImageTk

## Code

Python tkinter example

    import Tkinter
    import Image, ImageTk
    im = Image.open('pic.bmp')
    root = Tkinter.Tk()
    
    dither8 = [[ 0, 32,  8, 40,  2, 34, 10, 42],
               [48, 16, 56, 24, 50, 18, 58, 26],
               [12, 44,  4, 36, 14, 46,  6, 38],
               [60, 28, 52, 20, 62, 30, 54, 22],
               [ 3, 35, 11, 43,  1, 33,  9, 41],
               [51, 19, 59, 27, 49, 17, 57, 25],
               [15, 47,  7, 39, 13, 45,  5, 37],
               [63, 31, 55, 23, 61, 29, 53, 21]]
    
    dither8mod = [[64, 32,  8, 40,  2, 34, 10, 42],
                  [64, 16, 56, 24, 50, 18, 58, 26],
                  [64, 44,  4, 36, 14, 46,  6, 38],
                  [64, 28, 52, 20, 62, 30, 54, 22],
                  [64, 35, 11, 43,  1, 33,  9, 41],
                  [64, 19, 59, 27, 49, 17, 57, 25],
                  [64, 47,  7, 39, 13, 45,  5, 37],
                  [64, 31, 55, 23, 61, 29, 53, 21] ]
    
    
    sizex = im.size[0]
    sizey = im.size[1]
    im.size
    
    p = im.load()
    p
    p[0, 0][0]
    p[0, 0]
    
    for x in xrange(sizex):
        for y in xrange(sizey):
            p[x, y] = tuple((p[x, y][color] + ((32 - dither8[x%8][y%8]) * 2) // 150 * 150) for color in range(3))
    
    im.save('superlowficolor.bmp')
    
    tkimage = ImageTk.PhotoImage(im)
    Tkinter.Label(root,image=tkimage).pack()
    root.mainloop()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

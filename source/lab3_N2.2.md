---
title: lab3_N2.2
date: 2020-05-07
---
Example Python program lab3_N2.2.py

## Modules

* from graph import *

## Methods

* def fish(x, y, a, s, z):  # s - симметрия по оси Oy, z - симметрия относительно оси Ox
* def bear(x, y, a, s):  # s - симметрия по оси Oy

## Code

Python example

    from graph import *
    
    c = canvas()
    
    # BACKGROUND
    brushColor(0, 191, 255)
    rectangle(0, 0, 500, 350)
    
    penColor(0, 0, 0)
    brushColor(230, 230, 230)
    rectangle(0, 350, 500, 600)
    
    # ----------------------------------
    
    # SUN
    penColor('#FFEC8B')
    brushColor('#FFEC8B')
    circle(350, 150, 120)
    
    brushColor(0, 191, 255)
    penColor(0, 191, 255)
    circle(350, 150, 90)
    
    penColor('#FFEC8B')
    brushColor('#FFEC8B')
    circle(350, 150, 20)
    
    rectangle(230, 140, 470, 160)
    rectangle(340, 30, 360, 270)
    
    
    # ----------------------------------
    
    # FISH
    def fish(x, y, a, s, z):  # s - симметрия по оси Oy, z - симметрия относительно оси Ox
        penColor('black')
        brushColor('#ADADC7')
        polygon([(a * x, a * y), (a * (x + s * 30), a * (y - z * 10)), (a * x, a * (y - z * 20))])
        c.create_oval(a * (x + s * 30), a * y, a * (x + s * 100), a * (y - z * 20), fill='#ADADC7', outline='black')
        brushColor("#1E90FF")
        circle(a * (x + s * 80), a * (y - z * 10), a * 5)
        brushColor('black')
        circle(a * (x + s * 80), a * (y - z * 10), a * 2)
        penColor('white')
        brushColor('white')
        circle(a * (x + s * 78), a * (y - z * 12), a * 2)
        # верхний плавник
        penColor('black')
        brushColor('#CD5C5C')
        polygon([(a * (x + s * 80), a * (y - z * 19)), (a * (x + s * 82), a * (y - z * 27)),
                 (a * (x + s * 55), a * (y - z * 29)),
                 (a * (x + s * 65), a * (y - z * 20))])
        # нижний правый плавник
        polygon(
            [(a * (x + s * 80), a * (y - z * 1)), (a * (x + s * 82), a * (y + z * 8)), (a * (x + s * 69), a * (y + z * 8)),
             (a * (x + s * 70), a * y)])
        # нижний левый плавник
        polygon(
            [(a * (x + s * 50), a * (y - z * 1)), (a * (x + s * 49), a * (y + z * 8)), (a * (x + s * 35), a * (y + z * 8)),
             (a * (x + s * 40), a * (y - z * 2))])
    
    
    # ----------------------------------
    
    def bear(x, y, a, s):  # s - симметрия по оси Oy
        # POOL
        # water
        c.create_oval(a * (x + s * 320), a * (y + 430), a * (x + s * 470), a * (y + 480), fill='#555555', outline='black')
        # hole
        c.create_oval(a * (x + s * 330), a * (y + 440), a * (x + s * 460), a * (y + 480), fill='#008080', outline='black')
        # FISHES
        # under pool
        fish(x + s * 290, y + 550, a, s, 1)
        fish(x + s * 500, y + 550, a, s * (-1), 1)
        fish(x + s * 330, y + 530, a, s, 1)
        fish(x + s * 300, y + 510, a, s, 1)
        # above pool
        fish(x + s * 280, y + 400, a, s, -1)
        fish(x + s * 520, y + 400, a, s * (-1), -1)
        fish(x + s * 340, y + 410, a, s, 1)
        # ROD
        # stick
        penColor('black')
        penSize(a * 3)
        line(a * (x + s * 180), a * (y + 330), a * (x + s * 200), a * (y + 270))
        line(a * (x + s * 200), a * (y + 270), a * (x + s * 405), a * (y + 100))
        # rope
        penSize(a * 1)
        line(a * (x + s * 405), a * (y + 100), a * (x + s * 405), a * (y + 460))
        # BODY
        c.create_oval(a * (x + s * 5), a * (y + 200), a * (x + s * 180), a * (y + 500), fill='#e6e6e6', outline='black')
        # HEAD
        c.create_oval(a * (x + s * 80), a * (y + 150), a * (x + s * 190), a * (y + 210), fill='#e6e6e6', outline='black')
        # eye
        penColor('black')
        brushColor("black")
        circle(a * (x + s * 130), a * (y + 172), a * 3)
        # nose
        circle(a * (x + s * 190), a * (y + 173), a * 3)
        # mouse
        line(a * (x + s * 120), a * (y + 195), a * (x + s * 183), a * (y + 195))
        # ear
        brushColor("white")
        circle(a * (x + s * 95), a * (y + 162), a * 9)
        # ARM
        c.create_oval(a * (x + s * 150), a * (y + 255), a * (x + s * 210), a * (y + 285), fill='#e6e6e6', outline='black')
        # LEG
        c.create_oval(a * (x + s * 110), a * (y + 410), a * (x + s * 230), a * (y + 510), fill='#e6e6e6', outline='black')
        # FOOT
        c.create_oval(a * (x + s * 200), a * (y + 480), a * (x + s * 280), a * (y + 510), fill='#e6e6e6', outline='black')
    
    
    # ----------------------------------
    
    
    # PICTURE
    # right upper bear
    bear(2400, 1500, 0.2, -1)
    # central bear
    bear(950, 1100, 0.3, -1)
    # left bottom bear
    bear(0, 1400, 0.3, 1)
    # right bottom bear
    bear(900, 550, 0.6, -1)
    run()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

---
title: lab3_N2
date: 2020-05-07
---
Example Python program lab3_N2.py

## Modules

* from graph import *

## Methods

* def fish(x, y):  # FISH

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
    # POOL
    # water
    c.create_oval(320, 430, 470, 480, fill='#555555', outline='black')
    # hole
    c.create_oval(330, 440, 460, 480, fill='#008080', outline='black')
    # ----------------------------------
    # BEAR
    # ROD
    # stick
    penColor('black')
    penSize(3)
    line(180, 330, 200, 270)
    line(200, 270, 405, 100)
    # rope
    penSize(1)
    line(405, 100, 405, 460)
    # BODY
    c.create_oval(5, 200, 180, 500, fill='#e6e6e6', outline='black')
    # HEAD
    c.create_oval(80, 150, 190, 210, fill='#e6e6e6', outline='black')
    # eye
    penColor('black')
    brushColor("black")
    circle(130, 172, 3)
    # nose
    circle(190, 173, 3)
    # mouse
    line(120, 195, 183, 195)
    # ear
    brushColor("white")
    circle(95, 162, 9)
    # ARM
    c.create_oval(150, 255, 210, 285, fill='#e6e6e6', outline='black')
    # LEG
    c.create_oval(110, 410, 230, 510, fill='#e6e6e6', outline='black')
    # FOOT
    c.create_oval(200, 480, 280, 510, fill='#e6e6e6', outline='black')
    # ----------------------------------
    def fish(x, y):  # FISH
        brushColor('#ADADC7')
        polygon([(x, y), (x + 30, y - 10), (x, y - 20)])
        c.create_oval(x + 30, y, x + 100, y - 20, fill='#ADADC7', outline='black')
        brushColor("#1E90FF")
        circle(x + 80, y - 10, 5)
        brushColor('black')
        circle(x + 80, y - 10, 2)
        brushColor('white')
        circle(x + 78, y - 12, 2)
        # верхний плавник
        brushColor('#CD5C5C')
        polygon([(x + 80, y - 19), (x + 82, y - 27), (x + 55, y - 29), (x + 65, y - 20)])
        # нижний правый плавник
        polygon([(x + 80, y - 1), (x + 82, y + 8), (x + 69, y + 8), (x + 70, y)])
        # нижний левый плавник
        polygon([(x + 50, y - 1), (x + 49, y + 8), (x + 35, y + 8), (x + 40, y - 2)])
    
    fish(330, 530)
    
    
    
    run()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

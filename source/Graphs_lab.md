---
title: Graphs_lab
date: 2020-05-07
---
Example Python program Graphs_lab.py

## Modules

* from graph import *

## Code

Python example

    from graph import *
    
    """Город"""
    # x, y = 600, 800
    # # Window
    # windowSize(x, y)
    # # Background
    # canvasSize(x + 100, y + 100)
    # brushColor("grey")
    # rectangle(0, 0, x + 100, y + 100)
    # # Cloud
    """Дом с круглым окном"""
    # # Rectangle
    # penColor(255,0,255)
    # penSize(5)
    # brushColor("blue")
    # rectangle(100, 100, 300, 200)
    # Polygon
    # brushColor("yellow")
    # polygon([(100,100), (200,50), (300,100), (100,100)])
    # Circle
    # penColor("white")
    # brushColor("green")
    # circle(200, 150, 50)
    """Столбцы"""
    # x1, y1, x2, y2 = 100, 100, 300, 200
    # # The total number of lines in the frame
    # N = 10
    # # Frame
    # rectangle(x1, y1, x2, y2)
    # # Line spacing
    # h = (x2 - x1) / (N + 1)
    # x = x1 + h
    # for i in range(N):
    #     line(x, y1, x, y2)
    #     x += h
    """Злой смайлик"""
    # brushColor("yellow")
    # circle(210, 200, 100) # Голова
    # brushColor("black")
    # penSize(11)
    # line(110, 120, 195, 170) # Левая бровь
    # penSize(1)
    # brushColor("red")
    # circle(165, 180, 20) # Левый глаз
    # brushColor("black")
    # circle(165, 180, 8)
    # penSize(11)
    # line(230, 170, 310, 135) # Правая бровь
    # penSize(1)
    # brushColor("red")
    # circle(259, 180, 16) # Левый глаз
    # brushColor("black")
    # circle(259, 180, 7)
    # penSize(20)
    # line(210-50, 260, 210+50, 260) # Рот
    
    run()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

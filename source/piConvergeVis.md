---
title: piConvergeVis
date: 2020-05-07
---
Example Python program piConvergeVis.py

## Modules

* import tkinter
* import random
* import time

## Code

Python tkinter example

    """
    
    Suppose we create a 2 unit by 2 unit square.
    
    Suppose we drop that square's center on the origin point
    of a Cartesian graph.
    
    The area of this square is 4.
    
    Suppose we then create a 1 unit radius circle and drop
    the circle's center on the origin point of a Cartesian
    graph.
    
    The area of the circle is pi * 1 * 1 (or pi).
    
    If we drop a random dot somewhere on the square, the
    probability that it will land on the circle is pi/4.
    
    If we drop MANY random dots on the square, then we
    can predict that (n * pi) / 4 dots will also be in
    the circle.
    
    in_circle = (n * pi) / 4
    
    If we solve for pi, then we get this:
    
    pi = (in_circle * 4) / n
    
    As n approaches infinity, pi will equal 3.14159.
    
    """
    
    import tkinter
    import random
    import time
    
    window = 500
    border = 50
    radius = (window - border*2) // 2
    center = window // 2
    
    canvas = tkinter.Canvas(tkinter.Tk(), width=window, height=window)
    canvas.pack()
    
    canvas.create_oval(border, border, window-border, window-border, outline='red')
    canvas.create_rectangle(border, border, window-border, window-border, outline='blue')
    
    pi_text = tkinter.StringVar()
    pi_label = tkinter.Label(canvas, textvariable=pi_text)
    pi_label.place(x=border, y=window-border+10)
    
    in_circle = 0
    for n in range(1, 100000):
        x = random.random() * 2 - 1
        y = random.random() * 2 - 1
    
        p = x * radius + center
        q = y * radius + center
    
        if x*x + y*y < 1:
            in_circle += 1
            canvas.create_arc(p, q, p, q, outline='green')
        else:
            canvas.create_arc(p, q, p, q, outline='black')
    
        pi_text.set("pi = {:9f}  n = {:d}".format(in_circle * 4.0 / n, n))
        canvas.update()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

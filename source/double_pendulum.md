---
title: double_pendulum
date: 2020-05-07
---
Example Python program double_pendulum.py

## Modules

* import math, tkinter, time, sys

## Methods

* def theta1_2(v_theta1, v_theta2, theta1, theta2, g=9.8, m1=1, m2=1, l1=1, l2=1):
* def theta2_2(v_theta1, v_theta2, theta1, theta2, g=9.8, m1=1, m2=1, l1=1, l2=1):

## Code

Python tkinter example

    import math, tkinter, time, sys
    
    g = 9.8
    m1 = 1
    m2 = 1
    l1 = 150
    l2 = 150
    dt = 0.1
    theta1 = math.pi / 2
    theta2 = math.pi / 2 #+ 0.02
    v_theta1 = 0
    v_theta2 = 0
    
    mode = sys.argv[1]
    
    def theta1_2(v_theta1, v_theta2, theta1, theta2, g=9.8, m1=1, m2=1, l1=1, l2=1):
        return (g * (math.sin(theta2) * math.cos(theta1 - theta2) - (m1 + m2) / m2 * math.sin(theta1)) - (l1 * v_theta1**2 * math.cos(theta1 - theta2) + l2 * v_theta2**2) * math.sin(theta1 - theta2)) / (l1 * ((m1 + m2) / m2 - math.cos(theta1 - theta2)**2))
    
    def theta2_2(v_theta1, v_theta2, theta1, theta2, g=9.8, m1=1, m2=1, l1=1, l2=1):
        return (g * (m1 + m2) / m2 * (math.cos(theta1 - theta2) * math.sin(theta1) - math.sin(theta2)) + ((m1 + m2) / m2 * l1 * v_theta1**2 + l2 * math.cos(theta1 - theta2) * v_theta2**2) * math.sin(theta1 - theta2)) / (l2 * ((m1 + m2) / m2 - math.cos(theta1 - theta2)**2))
    
    c0 = tkinter.Canvas(width=640, height=480)
    c0.pack()
    x1 = 320 + l1 * math.sin(theta1)
    y1 = 150 + l1 * math.cos(theta1)
    x2 = x1 + l2 * math.sin(theta2)
    y2 = y1 + l2 * math.cos(theta2)
    c0.create_line(320, 150, x1, y1, tags="bar1", width=3.0)
    c0.create_line(x1, y1, x2, y2, tags="bar2", width=3.0)
    c0.update()
    time.sleep(3)
    
    for i in range(100000):
        a_theta1 = theta1_2(v_theta1, v_theta2, theta1, theta2, g, m1, m2, l1, l2)
        a_theta2 = theta2_2(v_theta1, v_theta2, theta1, theta2, g, m1, m2, l1, l2)
        v_theta1 += a_theta1 * dt
        v_theta2 += a_theta2 * dt
        theta1 += v_theta1 * dt
        theta2 += v_theta2 * dt
        x1 = 320 + l1 * math.sin(theta1)
        y1 = 150 + l1 * math.cos(theta1)
        x2 = x1 + l2 * math.sin(theta2)
        y2 = y1 + l2 * math.cos(theta2)
        if mode == "trajectory" and i > 0:
            c0.create_line(x0, y0, x2, y2, fill="red", smooth=True, tags="tj")
        c0.coords("bar1", 320, 150, x1, y1)
        c0.coords("bar2", x1, y1, x2, y2)
        x0 = x2
        y0 = y2
        time.sleep(dt*0.1)
        c0.update()
    tkinter.mainloop()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

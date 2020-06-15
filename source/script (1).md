---
title: script (1)
date: 2020-05-07
---
Example Python program script (1).py

## Modules

* import tkinter
* import time

## Methods

* def animation():
* def draw_point(x, y, c='black'):
* def transform(x, y):

## Code

Python tkinter example

    import tkinter
    import time
    
    master = tkinter.Tk()
    
    canvas = tkinter.Canvas(master, width=1000, height=1000)
    canvas.pack()
    
    def animation():
        def draw_point(x, y, c='black'):
            canvas.create_rectangle(x, y, x + 1, y + 1, fill=c)
    
        r = 200
        bottom_x, bottom_y = 500, 900
        tick = 0
        point_x, point_y = 500, 20
        point_speed_x = 10
        min_x, max_x = 20, 1000 - 20
        point_r = 5
        while True:
    
            prev_h = 0
            canvas.create_rectangle(0, 0, 1000, 1000, fill='white')
            for i in range(1, 2 * r + 1):
                curr_h = (r**2 - (r - i) ** 2) ** 0.5
                canvas.create_line(bottom_x + prev_h, bottom_y - i + 1,
                                   bottom_x + curr_h, bottom_y - i)
                canvas.create_line(bottom_x - prev_h, bottom_y - i + 1,
                                   bottom_x - curr_h, bottom_y - i)
                prev_h = curr_h
    
            canvas.create_oval(point_x - point_r, point_y - point_r,
                               point_x + point_r, point_y + point_r,
                               fill='red')
    
            canvas.create_line(bottom_x - r, bottom_y,
                               bottom_x + r, bottom_y)
            canvas.create_line(bottom_x - r, bottom_y - 2 * r,
                               bottom_x + r, bottom_y - 2 * r)
            canvas.create_line(bottom_x - r, bottom_y,
                               bottom_x - r, bottom_y - 2 * r)
            canvas.create_line(bottom_x + r, bottom_y,
                               bottom_x + r, bottom_y - 2 * r)
    
            def transform(x, y):
                scale = (bottom_y - y) / float(bottom_y - point_y)
                middle_x = bottom_x + (point_x - bottom_x) * scale
                return middle_x + (x - bottom_x) * (1 - scale), y
    
            canvas.create_line(*transform(bottom_x - r, bottom_y), point_x, point_y)
            canvas.create_line(*transform(bottom_x + r, bottom_y), point_x, point_y)
    
            canvas.create_line(*transform(bottom_x - r, bottom_y),
                               *transform(bottom_x + r, bottom_y))
            canvas.create_line(*transform(bottom_x - r, bottom_y - 2 * r),
                               *transform(bottom_x + r, bottom_y - 2 * r))
            canvas.create_line(*transform(bottom_x - r, bottom_y),
                               *transform(bottom_x - r, bottom_y - 2 * r))
            canvas.create_line(*transform(bottom_x + r, bottom_y),
                               *transform(bottom_x + r, bottom_y - 2 * r))
    
            prev_h = 0
            for i in range(1, 2 * r + 1):
                curr_h = (r**2 - (r - i) ** 2) ** 0.5
                canvas.create_line(*transform(bottom_x + prev_h, bottom_y - i + 1),
                                   *transform(bottom_x + curr_h, bottom_y - i),
                                   fill='red', width=2)
                canvas.create_line(*transform(bottom_x - prev_h, bottom_y - i + 1),
                                   *transform(bottom_x - curr_h, bottom_y - i),
                                   fill='red', width=2)
                prev_h = curr_h
    
            tick += 1
            point_x += point_speed_x
            if point_x >= max_x or point_x <= min_x:
                point_speed_x *= -1
            canvas.update()
            time.sleep(0.025)
    
    master.after(0, animation)
    tkinter.mainloop()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

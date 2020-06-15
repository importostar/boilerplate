---
title: circle_thing
date: 2020-05-07
---
Example Python program circle_thing.py

## Modules

* import tkinter as tk
* from tkinter import Canvas
* from math import log2, ceil

## Methods

* def draw_picture_recursive(radius: float, r_min: float=10) -> tk.Tk:
* def draw_circle(r: float, x: float, y: float) -> None:
* def draw_picture(r: float, x: float, y: float) -> None:
* def draw_picture_loop(radius: int, r_min: int=10) -> tk.Tk:
* def draw_circle(r: float, x: float, y: float) -> None:
* def highest_power_2_in(num: int) -> int:
* def draw_chunk(r: float, x: float, y: float) -> None:
* def draw_picture(r: float, x: float, y: float) -> None:

## Code

Python tkinter example

    import tkinter as tk
    from tkinter import Canvas
    from math import log2, ceil
    
    
    def draw_picture_recursive(radius: float, r_min: float=10) -> tk.Tk:
        """
        Draws the fractal pattern to a new tkinter window using recursion
        :param radius: the radius of the largest circle
        :param r_min: the cutoff radius. Smallest circle will be the first with radius <= r_min
        :return: the tkinter window
        """
        root = tk.Tk()
        root.title("recursive")
        canvas = Canvas(root, width=radius*4, height=radius*4)
        canvas.pack()
    
        def draw_circle(r: float, x: float, y: float) -> None:
            """Draws a circle on the canvas with center (x, y) and radius r"""
            canvas.create_oval(x-r, y-r, x+r, y+r)
    
        def draw_picture(r: float, x: float, y: float) -> None:
            """
            recursively draw the fractal pattern
            :param r: the radius of the larges circle at this step
            :param x: the center for this step
            :param y: the center for this step
            :return: None
            """
            draw_circle(r, x, y)
            if r > r_min:
                draw_picture(r/2, x-r, y)
                draw_picture(r/2, x+r, y)
                draw_picture(r/2, x, y-r)
                draw_picture(r/2, x, y+r)
    
        draw_picture(radius, radius*2, radius*2)
    
        return root
    
    
    def draw_picture_loop(radius: int, r_min: int=10) -> tk.Tk:
        """
        iteratively draws the fractal with no recursion
        :param radius: the max radius
        :param r_min: the minimum radius
        :return: the image window
        """
        root = tk.Tk()
        root.title("loop")
        canvas = Canvas(root, width=radius*4, height=radius*4)
        canvas.pack()
    
        def draw_circle(r: float, x: float, y: float) -> None:
            """Draws a circle on the canvas with center (x, y) and radius r"""
            canvas.create_oval(x-r, y-r, x+r, y+r)
        
        def highest_power_2_in(num: int) -> int:
            """Returns the highest power of 2 that exactly divides num"""
            return int(num) & -int(num)
    
        def draw_chunk(r: float, x: float, y: float) -> None:
            """iteratively draws the horizontal version of the fractal"""
            num = 2
            draw_circle(r, x, y)
            tot = r
            while r > r_min:
                old_r = r
                r /= 2
                for i in range(num):
                    draw_circle(r, x - tot + 2*i*old_r, y)
                num *= 2
                tot += r
        
        def draw_picture(r: float, x: float, y: float) -> None:
            """draws the 2d fractal centred at (x, y) with largest radius r"""
    
            # pre calculate the number of rows in the image and the size of the smallest circles
            pow_2 = ceil(log2(r/r_min))
            pic_min_radius = radius / 2**pow_2
            num_rows = 2**pow_2 - 1
    
            draw_chunk(r, x, y)
            for i in range(1, num_rows+1):
                # this is fortunately the depth of the fractal at this layer
                div_p2 = highest_power_2_in(i)
                # this is the number of times the pattern is repeated in this layer
                num = int(i / div_p2)
    
                # the correctly scaled radius at this row
                row_radius = pic_min_radius * div_p2
    
                # calculate y position of the row, each row is offset by the same amount, which is the diameter of the
                # smallest circles
                y_off = 2 * i * pic_min_radius
    
                # rows are mirrored about the centre
                y_offset_1 = x + 2*r - y_off
                y_offset_2 = x - 2*r + y_off
    
                # draw stuff
                for j in range(num):
                    j -= num//2
    
                    x_offset = 4 * j * row_radius
                    draw_chunk(row_radius, x + x_offset, y_offset_1)
                    draw_chunk(row_radius, x + x_offset, y_offset_2)
        
        draw_picture(radius, radius*2, radius*2)
        return root
    
    
    picture_1 = draw_picture_recursive(200)
    picture_1.update()
    picture_2 = draw_picture_loop(200)
    picture_2.mainloop()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

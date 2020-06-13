---
title: Sin_cos
date: 2020-05-07
---
Example Python program Sin_cos.py

## Modules

* import tkinter
* import math

## Methods

* def run():

## Code

Python tkinter example

    import tkinter
    import math
    
    # окно Tkinter
    tk = tkinter.Tk()
    
    # задаем размеры полотна
    width = 600
    height = 600
    
    # создаем область для рисования:
    canvas = tkinter.Canvas(tk, bg='white', height=height, width=width)
    
    angle_label = tkinter.Label(tk, foreground='green')
    cos_label = tkinter.Label(tk, foreground='blue')
    sin_label = tkinter.Label(tk, foreground='red')
    
    # располагаем нашу область в окне
    canvas.pack()
    
    angle_label.pack()
    cos_label.pack()
    sin_label.pack()
    
    radius = 200
    center_x = width / 2
    center_y = height / 2
    O = (center_x, center_y)
    angle = 0
    
    # рисуем координатные оси и окружность
    canvas.create_line((0, center_y), (width, center_y))
    canvas.create_line((center_x, 0), (center_x, height))
    
    top_left = (center_x - radius, center_y - radius)
    bottom_right = (center_x + radius, center_y + radius)
    canvas.create_oval(top_left, bottom_right)
    
    # основная функция анимации
    def run():
        global tk, canvas, angle, radius_S
    
        angle += 0.05
        x = center_x + radius * math.cos(angle)
        y = center_y + radius * math.sin(angle)
    
        A = (x,y)
        X = (x, center_y)
    
        # удаляем старые стрелки
        canvas.delete("arrows")
        # линия угла
        canvas.create_line(O, A, fill='green', width=3, tag='arrows')
        # линия синуса
        canvas.create_line(X, A, fill='red', width=3, tag='arrows')
        # линия косинуса
        canvas.create_line(O, X, fill='blue', width=3, tag='arrows')
    
        # подписи с данными
        angle_label['text'] = f'angle = {int(angle / math.pi * 180) % 360}'
        cos_label['text'] = f'cos = {math.cos(angle)}'
        sin_label['text'] = f'sin = {math.sin(angle)}'
    
        # удаляем старый текст
        canvas.delete("text")
        # подписи к вершинам
        canvas.create_text(center_x, center_y, text=f'O',
                           anchor='ne', tag='text')
        canvas.create_text(x, y, text=f'A',
                           anchor='n', tag='text')
        canvas.create_text(x, center_y, text=f'X',
                           anchor='n', tag='text')
    
        # повторо анимации: 30 кадров в секунду
        tk.after(1000 // 30, run)
    
    # запускаем функцию рисования
    run()
    
    # запусаем окно
    tk.mainloop()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

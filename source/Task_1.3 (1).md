---
title: Task_1.3 (1)
date: 2020-05-07
---
Example Python program Task_1.3 (1).py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import tkinter
* from random import choice, randint

## Methods

* def click_ball(event):
* def create_random_ball():
* def random_color():
* def init_ball_catch_game():
* def init_mail_window():

## Code

Python tkinter example

    import tkinter
    from random import choice, randint
    
    ball_initial_numder = 100
    ball_minimal_radius = 15
    ball_maximal_radius = 40
    ball_available_colors = ['green', 'blue', 'red', 'lightgray', '#FF00FF', '#FFFF00']
    
    def click_ball(event):
       # event.x, event.y)
       obj = canvas.find_closest(event.x, event.y)
       print(int(obj['x']), int(obj['y']))
       print(dir(obj))
        #if obj['x']
        #canvas.delete(obj)
    
    
    def create_random_ball():
        R = randint(ball_minimal_radius, ball_maximal_radius)
        x = randint(0, int(canvas['width'])-1-2*R)
        y = randint(0, int(canvas['height'])-1-2*R)
        canvas.create_oval(x, y, x+2*R, y+2*R,
                        width=1, fill=random_color())
    def random_color():
        return choice(ball_available_colors)
    
    def init_ball_catch_game():
        for i in range(ball_initial_numder):
            create_random_ball()
    
    
    def init_mail_window():
        global root,canvas
    
        root = tkinter.Tk()
        canvas = tkinter.Canvas(root, background='white',
                                width=400, height=400)
        canvas.bind("<Motion>", click_ball)
        canvas.pack()
    
    
    
    #for i in range(10):
    
    if __name__ == "__main__":
        init_mail_window()
        init_ball_catch_game()
        root.mainloop()
        print('Все the end.')

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

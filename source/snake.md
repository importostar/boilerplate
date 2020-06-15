---
title: snake
date: 2020-05-07
---
Example Python program snake.py

## Modules

* from collections import deque
* import functools
* import operator
* import time
* import tkinter
* from tkinter.constants import *
* import random

## Classes

* class point(tuple):
* class Snake(object):
* class Bounds(object):
* class Boon(object):
* class App(tkinter.Frame):

## Methods

* def __new__(cls, x, y):
* def _delegate_s(op):
* def f(self, other):
* def __neg__(self):
* def __mul__(self, other):
* def __truediv__(self, other):
* def all(self):
* def any(self):
* def __init__(self, app, startpos, direction, growth = 0):
* def ahead(self):
* def move(self):
* def grow(self, x):
* def check_collide(self, position):
* def render(self, canvas, subtick):
* def collide(self, app):
* def __init__(self, app, canvas):
* def render(self, canvas, subtick):
* def check_collide(self, position):
* def collide(self, app):
* def __init__(self, app):
* def check_collide(self, position):
* def pick(self, app):
* def render(self, canvas, subtick):
* def collide(self, app):
* def __init__(self, parent=None):
* def chdir(self, new_dir):
* def loop(self):

## Code

Python tkinter example

    # snake
    from collections import deque
    import functools
    import operator
    import time
    import tkinter
    from tkinter.constants import *
    import random
    
    class point(tuple):
        def __new__(cls, x, y):
            return tuple.__new__(cls, (x, y))
    
        def _delegate_s(op):
            def f(self, other):
                return point(op(self[0], other[0]), op(self[1], other[1]))
            return f
    
        for op in ('__add__', '__sub__',
                   '__lt__', '__le__',
                   '__gt__', '__ge__',
                   '__eq__', '__ne__'):
            f = _delegate_s(getattr(operator, op))
            f.__name__ = op
            vars()[op] = f
    
        def __neg__(self):
            return point(-self[0], -self[1])
    
        def __mul__(self, other):
            return point(self[0] * other, self[1] * other)
    
        def __truediv__(self, other):
            return point(self[0] / other, self[1] / other)
    
        def all(self):
            return all(self)
    
        def any(self):
            return any(self)
    
    class Snake(object):
        def __init__(self, app, startpos, direction, growth = 0):
            self.points = deque((startpos,))
            self.direction = direction
            self.growth = growth
            self.render_id = None
            self.eye_id = None
    
        def ahead(self):
            return self.points[-1] + self.direction
    
        def move(self):
            head = self.ahead()
            if self.growth:
                self.growth -= 1
            else:
                self.points.popleft()
            self.points.append(head)
    
        def grow(self, x):
            self.growth += x
    
        def check_collide(self, position):
            return any((x == position).all() for x in self.points)
    
        def render(self, canvas, subtick):
            i = 0
            L = len(self.points) - 1
            result = deque()
            for i in range(L + 1):
                from_, to = self.points[i], self.points[i+1] if i < L else self.points[i] + self.direction
                direction = (to - from_) / 2
                halfway = (to + from_) / 2
                backangle1 = point(-direction[0] - direction[1], direction[0] - direction[1])
                backangle2 = point(-direction[0] + direction[1], -direction[0] - direction[1])
                if i == 0:
                    shift = direction * (1 - 2*subtick) if self.growth == 0 else direction
                    result.append(halfway + backangle1 - shift)
                    result.appendleft(halfway + backangle2 - shift)
                else:
                    result.append(halfway + backangle1)
                    result.appendleft(halfway + backangle2)
                if i == L:
                    result.append(halfway - backangle2 - direction * (1 - 2 * subtick))
                    result.appendleft(halfway - backangle1 - direction * (1 - 2 * subtick))
                    eyecoord1 = halfway - backangle2 * 0.5 - direction * (1 - 2 * subtick)
                    eyecoord2 = halfway - backangle1 * 0.5 - direction * (1 - 2 * subtick)
                else:
                    result.append(halfway - backangle2)
                    result.appendleft(halfway - backangle1)
            res2 = [result[0]]
            line1s, line1e = result[0], result[1]
            for i in range(2, len(result), 2):
                line2s, line2e = result[i], result[i + 1]
                a, b, e = line1e[0] - line1s[0], line2s[0] - line2e[0], line2s[0] - line1s[0]
                c, d, f = line1e[1] - line1s[1], line2s[1] - line2e[1], line2s[1] - line1s[1]
                if a*d - b*c:
                    t = (e * d - b * f) / (a * d - b * c)
                    intersect = point(line1s[0] + a * t, line1s[1] + c * t)
                    res2.append(intersect)
                else:
                    res2.extend((line1e, line2s))
                line1s, line1e = line2s, line2e
            res2.append(line2e)
            points = [coord * 10 + 5 for point in res2 for coord in point]
            eye = lambda x: (x[0] * 10 + 5 - 1, x[1] * 10 + 5 - 1, x[0] * 10 + 5 + 1, x[1] * 10 + 5 + 1)
            if self.render_id:
                canvas.coords(self.render_id, *points)
                canvas.coords(self.eye_id[0], *eye(eyecoord1))
                canvas.coords(self.eye_id[1], *eye(eyecoord2))
            else:
                self.render_id = canvas.create_polygon(points, fill="#eeffee", outline="#00ff00")
                self.eye_id = (canvas.create_oval(*eye(eyecoord1), fill='black'),
                               canvas.create_oval(*eye(eyecoord2), fill='black'))
    
        def collide(self, app):
            if self.check_collide(self.ahead()):
                self.points = deque([self.points[-1]])
                self.growth = 1
                return True
            elif app.bounds.check_collide(self.ahead()):
                self.direction = -self.direction
                self.points = deque([self.points[-1]])
                self.growth = 1
                return True
    
    class Bounds(object):
        def __init__(self, app, canvas):
            w, h = int(canvas['width']), int(canvas['height'])
            self.upleft = point(1,1)
            self.downright = point(w//10-1, h//10-1)
            self.render_id = None
    
        def render(self, canvas, subtick):
            w, h = int(canvas['width']), int(canvas['height'])
            self.upleft = point(1,1)
            self.downright = point(w//10-1, h//10-1)
            x1, y1, x2, y2 = 9, 9, w - w%10 + 1, h - h%10 + 1
            if self.render_id:
                canvas.coords(self.render_id, x1, y1, x2, y2)
            else:
                self.render_id = canvas.create_rectangle(x1, y1, x2, y2, width=2, outline="#4444ff")
    
        def check_collide(self, position):
            return (position < self.upleft).any() or (position > self.downright).any()
    
        def collide(self, app):
            pass
    
    
    class Boon(object):
        def __init__(self, app):
            self.render_id = None
            self.position = point(-1, -1)
            self.pick(app)
    
        def check_collide(self, position):
            return (self.position == position).all()
    
        def pick(self, app):
            xmin, ymin = map(int, app.bounds.upleft)
            xmax, ymax = map(int, app.bounds.downright)
            oldpos = self.position
            snake = app.snake
            while True:
                pos = point(random.randint(xmin, xmax), random.randint(ymin, ymax))
                if not snake.check_collide(pos) and not (oldpos == pos).all():
                    self.position = pos
                    break
    
        def render(self, canvas, subtick):
            x, y = self.position
            coords = (x * 10 + 2, y * 10 + 2,
                      x * 10 + 8, y * 10 + 8)
            if not self.render_id:
                self.render_id = canvas.create_oval(*coords,
                                                    fill = "#ffeeee", outline = "#ff0000")
            else:
                canvas.coords(self.render_id, *coords)
    
        def collide(self, app):
            if self.check_collide(app.snake.ahead()):
                app.snake.grow(2)
                self.pick(app)
                return True
    
    
    class App(tkinter.Frame):
        def __init__(self, parent=None):
            super().__init__(parent)
            self.canvas = cv = tkinter.Canvas(self)
            cv.pack(expand = YES, fill = BOTH)
            self.time_rate = 0.3
            self.subtick = 0
            self.direction = point(1, 0)
            self.snake = Snake(self, point(5, 5), self.direction, 3)
            self.bounds = Bounds(self, cv)
            self.boon = Boon(self)
            self.bind_all("<Up>", lambda e: self.chdir(point(0, -1)))
            self.bind_all("<Down>", lambda e: self.chdir(point(0, 1)))
            self.bind_all("<Left>", lambda e: self.chdir(point(-1, 0)))
            self.bind_all("<Right>", lambda e: self.chdir(point(1, 0)))
            self.last_time = None
            self.snakeid = None
            self.after(0, self.loop)
    
        def chdir(self, new_dir):
            if (-self.snake.direction == new_dir).all():
                return
            self.direction = new_dir
    
        def loop(self):
            t = time.monotonic()
            if self.last_time is None:
                self.last_time = t
            else:
                self.subtick += (t - self.last_time) / self.time_rate
                self.last_time = t
            while self.subtick >= 1:
                self.snake.move()
                self.snake.direction = self.direction
                self.subtick -= 1
                if self.snake.collide(self):
                    self.time_rate = 0.3
                if self.boon.collide(self):
                    self.time_rate /= 1.1
                self.direction = self.snake.direction
            self.snake.render(self.canvas, self.subtick)
            self.bounds.render(self.canvas, self.subtick)
            self.boon.render(self.canvas, self.subtick)
            self.after(50, self.loop)
            
    
    root = tkinter.Tk()
    app = App(root)
    app.pack(expand=YES, fill=BOTH)
    root.mainloop()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

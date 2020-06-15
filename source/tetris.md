---
title: tetris
date: 2020-05-07
---
Example Python program tetris.py
For Python version 2.x.
To test your Python version use:

    python --version

## Modules

* import Tkinter
* import random
* import sys

## Classes

* class TetrisBlock():
* class Tetris():

## Methods

* def __init__(self, tetris, i=None):
* def move_box(self, box, x, y):
* def move_shape(self, x, y):
* def fall(self):
* def move(self, x, y):
* def rotate(self):
* def check(box):
* def __init__(self, width, height, ppb=30):
* def show(self):
* def game_frame(self):
* def key_press(self, e):

## Code

Python tkinter example

    #!/usr/bin/env python2
    
    import Tkinter
    import random
    import sys
    
    # Represents one block in tetris
    class TetrisBlock():
    
        SHAPES = [[(0,0), (1,0), (0,1), (1,1)], # BOX
                  [(0,0), (1,0), (2,0), (3,0)], # LINE
                  [(2,0), (0,1), (1,1), (2,1)], # Right L
                  [(0,0), (0,1), (1,1), (2,1)], # Left L
                  [(0,1), (1,1), (1,0), (2,0)], # Right S
                  [(0,0), (1,0), (1,1), (2,1)], # Left S
                  [(1,0), (0,1), (1,1), (2,1)]] # Pyramide
    
        COLORS = ["yellow","lightblue","orange","blue","green","red","purple"]
    
        def __init__(self, tetris, i=None):
            if i is None: i = random.randint(0,6)
            self.shape = self.SHAPES[i]
            self.color = self.COLORS[i]
            self.tetris = tetris
            self.canvas = self.tetris.canvas
            self.boxes = []
    
            mid = self.tetris.p_width / 2 - self.tetris.ppb / 2
    
            for point in self.shape:
                x,y = point
                box = self.canvas.create_rectangle(x * self.tetris.ppb + mid,
                                                   y * self.tetris.ppb,
                                                   (x+1) * self.tetris.ppb + mid,
                                                   (y+1) * self.tetris.ppb,
                                                   fill = self.color)
                self.boxes += [box]
    
        def move_box(self, box, x, y):
            x *= self.tetris.ppb
            y *= self.tetris.ppb
            coords = self.canvas.coords(box)
    
            if coords[3] + y > self.tetris.p_height: return False
            if coords[0] + x < 0: return False
            if coords[2] + x > self.tetris.p_width: return False
    
            o = set(self.canvas.find_overlapping((coords[0] + coords[2]) / 2 + x,
                                                 (coords[1] + coords[3]) / 2 + y,
                                                 (coords[0] + coords[2]) / 2 + x,
                                                 (coords[1] + coords[3]) / 2 + y ))
    
            other = set(self.canvas.find_all()) - set(self.boxes)
            if o & other: return False
    
            return True
    
        def move_shape(self, x, y):
            for box in self.boxes:
                if not self.move_box(box, x,y): return False
            return True
    
        def fall(self):
            if self.move_shape(0,1):
                for box in self.boxes:
                    self.canvas.move(box,0,self.tetris.ppb)
                return True
            return False
    
        def move(self, x, y):
            if not self.move_shape(x, y): return False
            else:
                for box in self.boxes:
                    self.canvas.move(box, x * self.tetris.ppb, y * self.tetris.ppb)
                return True
    
        def rotate(self):
            copy = self.boxes[:]
            pivot = copy.pop(2)
    
            def check(box):
                bc = self.canvas.coords(box)
                pc = self.canvas.coords(pivot)
                xd = bc[0] - pc[0]
                yd = bc[1] - pc[1]
                xm = (-xd-yd) / self.tetris.ppb
                ym = (xd-yd) / self.tetris.ppb
                return xm, ym
    
            # Check if all blocks can be rotated
            for box in copy:
                x,y = check(box)
                if not self.move_box(box,x,y):
                    return False
    
            # Move blocks
            for box in copy:
                x,y = check(box)
                self.canvas.move(box, x * self.tetris.ppb, y * self.tetris.ppb)
    
            return True
    
    
    # Tetris game
    class Tetris():
    
        def __init__(self, width, height, ppb=30):
            self.width = width
            self.height = height
            self.ppb = ppb
    
            # Calculate pixel dimensions
            self.p_width = self.width * self.ppb
            self.p_height = self.height * self.ppb
    
            # Game variables
            self.boxes = []
            self.c_box = None
            self.speed = 300
    
        # Show the UI
        def show(self):
            self.ui = Tkinter.Tk()
            self.ui.title("PyTetris")
    
            self.canvas = Tkinter.Canvas(self.ui, width=self.p_width,
                                                  height=self.p_height)
    
            self.canvas.pack()
    
            self.ui.bind("<Key>", self.key_press)
            self.game_frame()
    
            # Enter Tkinter mainloop
            self.ui.mainloop()
    
        # Render one game frame
        def game_frame(self):
            if self.c_box is None:
                self.c_box = TetrisBlock(self)
    
            if not self.c_box.fall():
                # Remove completed lines # TODO
                self.c_box = TetrisBlock(self)
    
                # Check gameover
                for box in self.c_box.boxes:
                    if not self.c_box.move_box(box, 0, 1):
                        print "Game over!"
                        sys.exit()
    
            self.ui.after(self.speed, self.game_frame)
    
        # Handle keypresses
        def key_press(self, e):
            if self.c_box is None: return
            if e.keysym == "Left": self.c_box.move(-1,0)
            if e.keysym == "Right": self.c_box.move(1,0)
            if e.keysym == "Down": self.c_box.move(0,1)
            if e.keysym == "Up": self.c_box.rotate()
    
    if __name__ == "__main__":
        t = Tetris(10,20)
        t.show()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

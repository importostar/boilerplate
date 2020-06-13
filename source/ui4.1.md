---
title: ui4.1
date: 2020-05-07
---
Example Python program ui4.1.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import tkinter as tk
* import test
* import wumpus_class
* import random
* import sys
* import os

## Classes

* class Wumpus(tk.Tk):

## Methods

*    def __init__(self, **kwargs):
*    def donothing(self):
*    def about(self):
*    def select_diff(self):
*    def button_up(self):
*    def button_down(self):
*    def button_left(self):
*    def button_right(self):
*    def button_shoot(self):
*    def button_move(self):
*    def updategrid(self):
*    def move_wumpus(self):
*    def shoot(self):
*    def message(self):
*    def loose(self):
*    def win(self):
*    def restart():

## Code

Python tkinter example

    #!/usr/bin/env python
    import tkinter as tk
    import test
    import wumpus_class
    import random
    import sys
    import os
    
    
    
    
    class Wumpus(tk.Tk):
       def __init__(self, **kwargs):
            super().__init__(**kwargs)
    
    #______________________________________add constants__________________________________________________
    
    
    
            self.difficulty = tk.IntVar()
            self.difficulty.set(0)
            self.select_diff()
    
            self.settings = test.setup(self.difficulty.get())
            self.alive = True
            num_rooms = 40
            parts = 4
            rum = []
            self.y_pos = 0
            self.x_pos = 0
            val = 0
            self.room = wumpus_class.rum(rum,parts,self.x_pos,self.y_pos)
    
            self.maze = test.spawn_room(parts,self.room)[1]
            rum = test.spawn_room(parts,self.room)[0]
            self.faror, self.w_y_pos, self.w_x_pos = test.spawn_danger(rum, self.maze, self.settings)
    
            self.y_pos = test.spawn_player(self.maze, self.faror)[0]
            self.x_pos = test.spawn_player(self.maze, self.faror)[1]
            adjucent = test.adjucent(self.y_pos,self.x_pos, self.maze, self.room)
    
            self.mode_shoot = False
            self.mode_move = True
            
    
    #______________________________________add frames__________________________________________________
            
            self.title("Wumpus")
            self.configure(background='white')
    
            global frame
            frame = tk.Frame()
            frame.pack(side=tk.LEFT,fill=tk.Y)
    
            frame2 = tk.Frame(self)
            frame2.pack(side=tk.RIGHT,fill=tk.Y)
    
            frame3 = tk.Frame(frame2)
            frame3.pack(side=tk.TOP)
    
            frame4 = tk.Frame(frame2)
            frame4.pack(side=tk.BOTTOM)
    
    #______________________________________add menu__________________________________________________
            
            menubar = tk.Menu(self)
            filemenu = tk.Menu(menubar, tearoff=0)
            filemenu.add_command(label="Restart", command=Wumpus.restart)
    
            filemenu.add_separator()
    
            filemenu.add_command(label="Exit", command=quit)
            menubar.add_cascade(label="File", menu=filemenu)
    
    
            helpmenu = tk.Menu(menubar, tearoff=0)
            helpmenu.add_command(label="Help Index", command=self.donothing)
            helpmenu.add_command(label="About...", command=self.about)
            menubar.add_cascade(label="Help", menu=helpmenu)
    
            self.config(menu=menubar)
    
    #______________________________________add variables__________________________________________________
            
            global message
            message = tk.StringVar()
            message.set("Welcome")
    
            global color
            color = tk.StringVar()
            color.set("light grey")
    
            global num_a
            self.num_a = tk.IntVar()
            self.num_a.set(0)
            
    
    
            self.title("Wumpus")
            
    #______________________________________add widgets__________________________________________________
            
            text = tk.Message(frame3, textvariable = message , bg = "white", relief=tk.RIDGE, width =  250, pady= 10, justify = tk.LEFT, anchor = tk.W)
            text.grid(row=0,column=0,sticky= tk.W + tk.E)
    
            lbl = tk.Label(frame3, text="Arrows", relief=tk.RIDGE,width=40,height=2,anchor= tk.W)
            lbl.grid(row=1,column=0)
            
            btn = tk.Button(frame4,text="Up", relief=tk.RAISED,width=8,height=4, command = self.button_up)
            btn.grid(row=2,column=5)
            btn = tk.Button(frame4,text="Down", relief=tk.RAISED,width=8,height=4, command = self.button_down)
            btn.grid(row=5,column=5)
            btn = tk.Button(frame4,text="Left", relief=tk.RAISED,width=8,height=4, command = self.button_left)
            btn.grid(row=5,column=4)
            btn = tk.Button(frame4,text="Right", relief=tk.RAISED,width=8,height=4, command = self.button_right)
            btn.grid(row=5,column=6)
    
            btn = tk.Button(frame4,text="Shoot", bg = "white", relief=tk.RAISED,width=8,height=4, command = self.button_shoot)
            btn.grid(row=2,column=6)
            btn = tk.Button(frame4,text="Move", bg = "white", relief=tk.RAISED,width=8,height=4, command = self.button_move)
            btn.grid(row=2,column=4)
    
            Wumpus.updategrid(self)
            Wumpus.message(self)
    
    #______________________________________functions__________________________________________________
    
       def donothing(self):
            filewin = tk.Toplevel(self)
            button = tk.Button(filewin, text="Do nothing button")
            button.pack()
    
       def about(self):
            filewin = tk.Toplevel(self)
            about_dev = tk.Label(filewin, text="Skapat utav Carl Svinge", width=40,height=20)
            about_dev.pack()
    
       def select_diff(self):
          
            filewin = tk.Toplevel(self)
            filewin.title("Select difficulty")
            filewin.attributes("-topmost", True)
            lbl = tk.Label(filewin, text = "Select\nDifficulty")
            lbl.pack(fill=tk.X)
            lbl.config(font=("Courier", 44))
            easy = tk.Button(filewin, text="Easy", command=lambda: self.difficulty.set(1), height = 3)
            medium = tk.Button(filewin, text="Medium", command=lambda: self.difficulty.set(2), height = 3)
            hard = tk.Button(filewin, text="Hard", command=lambda: self.difficulty.set(3), height = 3)
            easy.pack(fill=tk.X)
            medium.pack(fill=tk.X)
            hard.pack(fill=tk.X)
    
            filewin.wait_variable(self.difficulty)
            filewin.destroy()
    
    
       def button_up(self):
    
            if self.mode_move == True:
                self.y_pos, self.x_pos = test.move(self.y_pos,self.x_pos,self.maze,"n", self.room)
            
                Wumpus.message(self)
                Wumpus.move_wumpus(self)
                Wumpus.updategrid(self)
    
    
            elif self.mode_shoot == True:         
    
                self.a_y_pos, self.a_x_pos = test.move(self.a_y_pos,self.a_x_pos,self.maze,"n", self.room)
                
                self.shoot()
    
    
       def button_down(self):
    
            if self.mode_move == True:
                self.y_pos, self.x_pos = test.move(self.y_pos,self.x_pos,self.maze,"s", self.room)
            
                Wumpus.message(self)
                Wumpus.move_wumpus(self)
                Wumpus.updategrid(self)
    
    
            elif self.mode_shoot == True:         
    
                self.a_y_pos, self.a_x_pos = test.move(self.a_y_pos,self.a_x_pos,self.maze,"s", self.room)
                
                self.shoot()
    
                
       def button_left(self):
    
            if self.mode_move == True:
                self.y_pos, self.x_pos = test.move(self.y_pos,self.x_pos,self.maze,"a", self.room)
            
                Wumpus.message(self)
                Wumpus.move_wumpus(self)
                Wumpus.updategrid(self)
    
    
            elif self.mode_shoot == True:         
    
                self.a_y_pos, self.a_x_pos = test.move(self.a_y_pos,self.a_x_pos,self.maze,"a", self.room)
                
                self.shoot()
    
    
       def button_right(self):
    
            if self.mode_move == True:
                self.y_pos, self.x_pos = test.move(self.y_pos,self.x_pos,self.maze,"d", self.room)
            
                Wumpus.message(self)
                Wumpus.move_wumpus(self)
                Wumpus.updategrid(self)
    
    
            elif self.mode_shoot == True:         
    
                self.a_y_pos, self.a_x_pos = test.move(self.a_y_pos,self.a_x_pos,self.maze,"d", self.room)
                
                self.shoot()
    
    
       def button_shoot(self):
          
          text, self.a_y_pos, self.a_x_pos = test.arrow(self.y_pos,self.x_pos, self.num_a.get())
          message.set(text)
          self.mode_shoot = True
          self.mode_move = False
    
       def button_move(self):
            self.mode_shoot = False
            self.mode_move = True
            
    
       def updategrid(self):
                    
            for r, c in enumerate(self.maze):
                for col in range(5):
                    
                    if self.maze[r][col] == self.maze[self.y_pos][self.x_pos]:
                        color.set("grey")
                        
                    elif self.maze[r][col] in self.faror[0]:
                        
                        color.set("green")
                    elif self.maze[r][col] in self.faror[1]:
                        
                        color.set("blue")
    
                    elif self.maze[r][col] == self.maze[self.w_y_pos][self.w_x_pos]:
                      
                        color.set("red")
    
                    else:
                        color.set("light grey")
    
                    lbl = tk.Label(frame, text=str(self.maze[r][col]), relief=tk.RIDGE,width=10,height=5, bg = color.get())
    
                    lbl.grid(row=r,column=col)
    
       def move_wumpus(self):
          
          if self.settings[0] == True:
             
             val = random.randint(1,4)
             if val == 1: val = "n"
             if val == 2: val = "s"
             if val == 3: val = "a"
             if val == 4: val = "d"
             self.w_y_pos, self.w_x_pos = test.move(self.w_y_pos,self.w_x_pos,self.maze,val, self.room)
    
    
    
       def shoot(self):
          
          x = self.num_a.get()
          x += 1
    
    
          self.a_pos = self.maze[self.a_y_pos][self.a_x_pos]
    
          if self.a_pos == self.maze[self.w_y_pos][self.w_x_pos]:
    
             self.win()
          
          elif x >= 3:
    
             self.mode_move = True
             message.set("Du missade")
             self.num_a.set(0)
    
          else:
    
             self.num_a.set(x)
    
             text = test.arrow(self.a_y_pos,self.a_x_pos, self.num_a.get())[0]
             message.set(text)
    
             
    
       def message(self):
    
          adjucent = test.adjucent(self.y_pos,self.x_pos, self.maze, self.room)
          text, self.y_pos, self.x_pos, self.alive = test.danger(adjucent,self.faror, self.maze, self.y_pos, self.x_pos, self.alive)
          text = text["vind"]+text["fladdermöss"]+text["wumpus"]+text["dead"]
    
          message.set(text)
    
          if self.alive == False:
             self.loose()
    
    
       def loose(self):
          
            self.title("Game Over")
            filewin = tk.Toplevel(self)
            filewin.attributes("-topmost", True)
            lbl = tk.Label(filewin, text = "You died!")
            lbl.pack(fill=tk.X)
            lbl.config(font=("Courier", 44))
            leave = tk.Button(filewin, text="Quit Game", command = quit, width = 20, height = 5)
            leave.pack(fill=tk.X)
            restart = tk.Button(filewin, text="Restart", command = Wumpus.restart, width = 20, height = 5)
            restart.pack(fill=tk.X) 
    
    
       def win(self):
    
          filewin = tk.Toplevel(self)
          filewin.title("Win")
          filewin.attributes("-topmost", True)
          lbl = tk.Label(filewin, text = "You Win!")
          lbl.pack(fill=tk.X)
          lbl.config(font=("Courier", 44))
          leave = tk.Button(filewin, text="Quit Game", command = quit, width = 20, height = 5)
          leave.pack(fill=tk.X)
          restart = tk.Button(filewin, text="Restart", command = Wumpus.restart, width = 20, height = 5)
          restart.pack(fill=tk.X)
    
    
    
       def restart():
    
          
          python = sys.executable
          print(python)
          print(* sys.argv)
          os.execl(python, python, * sys.argv)
          #os.execv(sys.executable, ['python'] + sys.argv)
          #os.execv(__file__, sys.argv)
    
    if __name__ == '__main__':
    
        gui = Wumpus()
        gui.mainloop()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

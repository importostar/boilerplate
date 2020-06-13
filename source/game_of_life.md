---
title: game_of_life
date: 2020-05-07
---
Example Python program game_of_life.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* # from __future__ import print_function
* import tkinter as tk
* from tkinter import *
* from tkinter import messagebox
* import numpy as np
* import _thread
* import time
* import json
* import sys

## Classes

* class GUI:
* class Game:

## Methods

* 	def __init__(self, num_rows, num_cols, px_per_box, bg_color, cell_color, line_wid=0):
* 	def on_closing(self):
* 	def init_info(self):
* 	def init_dimensions(self, num_rows, num_cols):
* 	def init_canvas(self):
* 	def create_grid(self):
* 	def create_rectangles(self):
* 	def update(self, config):
* 	def make_info(self, config):
* 	def update_info(self, config):
* 	def update_canvas(self, config):
* 	def __init__(self, num_rows, num_cols, config):
* 	def init_config(self):
* 	def load_config(self, config):
* 	def get_neighbours(self, state):
* 	def gen_next_state(self):
* 	def step(self):
* def get_config(file):
* def load_preset(config, preset):

## Code

Python tkinter example

    # for Python 2 just uncomment the line below
    # from __future__ import print_function
    import tkinter as tk
    from tkinter import *
    from tkinter import messagebox
    
    import numpy as np
    import _thread
    import time
    import json
    import sys
    
    class GUI:
    	def __init__(self, num_rows, num_cols, px_per_box, bg_color, cell_color, line_wid=0):
    		self.root 		= Tk()
    		self.steps 		= 0
    		self.line_wid   = line_wid
    		self.px_per_box = px_per_box
    		self.bg_color 	= bg_color
    		self.cell_color = cell_color
    		self.to_update	= True
    		self.boxes 		= np.zeros((num_rows, num_cols), dtype=object)
    		self.init_dimensions(num_rows, num_cols)
    		self.init_canvas()
    		self.create_grid()
    		self.create_rectangles()
    		self.init_info()
    		self.root.protocol("WM_DELETE_WINDOW", self.on_closing)
    		self.root.title("Conway's Game of life")
    
    	def on_closing(self):
    		self.to_update = False
    		if messagebox.askokcancel("Quit", "Do you want to quit?"):
    			self.root.destroy()
    		else:
    			self.to_update = True
    
    	def init_info(self):
    		self.info		= Label(self.root, text="", height=2, width=self.num_cols)
    		self.info.pack(side=BOTTOM)
    
    	def init_dimensions(self, num_rows, num_cols):
    		self.num_rows   = num_rows
    		self.num_cols   = num_cols
    		self.width      = self.num_cols*self.px_per_box + (self.num_cols + 1)*self.line_wid
    		self.height     = self.num_rows*self.px_per_box + (self.num_rows + 1)*self.line_wid
    
    	def init_canvas(self):
    		self.canvas = Canvas(self.root, width=self.width, height=self.height)
    		self.canvas.pack()
    		
    	def create_grid(self):
    		for i in range(self.num_cols+1):
    			col = (self.line_wid + self.px_per_box)*i + self.line_wid/2
    			self.canvas.create_line(col, 0, col, self.height, width=self.line_wid)
    		for i in range(self.num_rows+1):
    			row = (self.line_wid + self.px_per_box)*i + self.line_wid/2
    			self.canvas.create_line(0, row, self.width, row, width=self.line_wid)
    
    	def create_rectangles(self):
    		for i in range(self.num_rows):
    			for j in range(self.num_cols):
    				y1 = i*self.px_per_box + (i + 1)*self.line_wid
    				x1 = j*self.px_per_box + (j + 1)*self.line_wid
    				self.boxes[i,j] = self.canvas.create_rectangle(x1, y1, \
    					x1+self.px_per_box, y1+self.px_per_box, fill=self.bg_color)
    	def update(self, config):
    		self.steps += 1
    		self.update_canvas(config)
    		self.update_info(config)
    		if self.to_update:
    			self.root.update()
    
    	def make_info(self, config):
    		population = len(np.nonzero(config)[0])
    		str = "Population:\t{}\nTime Steps:\t{}"
    		str = str.format(population, self.steps)
    		return str
    
    
    	def update_info(self, config):
    		info = self.make_info(config)
    		self.info.configure(text=info)
    
    	def update_canvas(self, config):
    		for i in range(self.num_rows):
    			for j in range(self.num_cols):
    				color = self.bg_color
    				if config[i,j]:
    					color = self.cell_color
    				self.canvas.itemconfig(self.boxes[i,j], fill=color)
    
    class Game:
    	def __init__(self, num_rows, num_cols, config):
    		self.num_rows = num_rows
    		self.num_cols = num_cols
    		self.init_config()
    		self.load_config(config)
    
    	def init_config(self):
    		self.next_config = np.zeros((self.num_rows, self.num_cols), dtype=bool)
    		self.prev_config = np.zeros((self.num_rows, self.num_cols), dtype=bool)
    
    	def load_config(self, config):
    		init_state = config
    		st_r = (self.prev_config.shape[0] - init_state.shape[0])//2
    		en_r = (self.prev_config.shape[0] + init_state.shape[0])//2
    		st_c = (self.prev_config.shape[1] - init_state.shape[1])//2
    		en_c = (self.prev_config.shape[1] + init_state.shape[1])//2
    		self.prev_config[st_r:en_r, st_c: en_c] = init_state
    
    	def get_neighbours(self, state):
    		rolls = [np.roll(np.roll(state,i,0),j,1) \
    				for i in [-1,0,1] for j in [-1,0,1] if i!=0 or j!=0]
    		return sum(rolls)
    
    	def gen_next_state(self):
    		num_nbrs = self.get_neighbours(self.prev_config)
    		statis = self.prev_config*(num_nbrs > 1)*(num_nbrs < 4)
    		newgen = np.logical_not(self.prev_config)*(num_nbrs > 2)*(num_nbrs < 4)
    		self.next_config = statis + newgen
    
    	def step(self):
    		self.gen_next_state()
    		self.prev_config[:,:] = self.next_config
    
    def get_config(file):
    	f = open(file, 'r')
    	try:
    		return json.loads(f.read())
    	except:
    		print('Exception in JSON file')
    		return
    
    def load_preset(config, preset):
    	try:
    		init_state = config['Presets'][preset]
    		return np.array(init_state)
    	except KeyError as e:
    		print("No Preset {} in config file.".format(e), file=sys.stderr)
    		sys.exit(-1)
    
    if __name__ == '__main__':
    	config_file = sys.argv[1]
    	config = get_config(config_file)
    	if isinstance(config, type(None)):
    		sys.exit(-1)
    
    	num_rows 	= config['Game']['Rows']
    	num_cols 	= config['Game']['Columns']
    	time_step	= config['Game']['TimeStep']
    	preset		= config['Game']['Preset']
    
    	px_per_box 	= config['GUI']['CellDimension']
    	bg_color 	= config['GUI']['BackgroundColor']
    	cell_color	= config['GUI']['CellColor']
    	init_state 	= load_preset(config, preset)
    
    	if np.any(np.array(init_state.shape) > np.array([num_rows, num_cols])):
    		print("Preset {} shape {} is greater than grid {}"\
    			.format(preset, init_state.shape,(num_rows, num_cols)))
    		sys.exit(-1)
    
    	game 		= Game(num_rows, num_cols, init_state)
    	gui 		= GUI(num_rows, num_cols, px_per_box, bg_color, cell_color)
    	gui.update(game.prev_config)
    	
    	while gui.to_update:
    		time.sleep(time_step)
    		game.step()
    		gui.update(game.prev_config)

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

---
title: tictactoe
date: 2020-05-07
---
Example Python program tictactoe.py

## Modules

* from tkinter import *
* import tkinter.messagebox

## Classes

* class TicTacToe():

## Methods

* 	def __init__(self, tic):
* 	def check_victory(self):
* 	def click(self, button):
* 	def disable_button(self):

## Code

Python tkinter example

    from tkinter import *
    import tkinter.messagebox
    
    tic = Tk()
    tic.geometry("384x396")
    tic.title('Tic Tac Toe')
    tic.resizable(False, False)
    
    class TicTacToe():
    	def __init__(self, tic):
    		# Change the button text
    		self.bclick=True
    		self.flag=0
    		# Font
    		self.font = ('Times', '30', 'bold')
    		# Creating the buttons 
    		self.b1 = Button(tic, text='', font=self.font, height=2, width=5, command=lambda: self.click(self.b1))
    		self.b1.grid(row=2, column=0)
    
    		self.b2 = Button(tic, text='', font=self.font, height=2, width=5, command=lambda: self.click(self.b2))
    		self.b2.grid(row=2, column=1)
    
    		self.b3 = Button(tic, text='', font=self.font, height=2, width=5, command=lambda: self.click(self.b3))
    		self.b3.grid(row=2, column=2)
    	
    		self.b4 = Button(tic, text='', font=self.font, height=2, width=5, command=lambda: self.click(self.b4))
    		self.b4.grid(row=3, column=0)
    
    		self.b5 = Button(tic, text='', font=self.font, height=2, width=5, command=lambda: self.click(self.b5))
    		self.b5.grid(row=3, column=1)
    
    		self.b6 = Button(tic, text='', font=self.font, height=2, width=5, command=lambda: self.click(self.b6))
    		self.b6.grid(row=3, column=2)
    
    		self.b7 = Button(tic, text='', font=self.font, height=2, width=5, command=lambda: self.click(self.b7))
    		self.b7.grid(row=4, column=0)
    
    		self.b8 = Button(tic, text='', font=self.font, height=2, width=5, command=lambda: self.click(self.b8))
    		self.b8.grid(row=4, column=1)
    
    		self.b9 = Button(tic, text='', font=self.font, height=2, width=5, command=lambda: self.click(self.b9))
    		self.b9.grid(row=4, column=2)
    
    	def check_victory(self):
    		if (self.b1['text'] == 'X' and self.b2['text'] == 'X' and self.b3['text'] == 'X' or
    		    self.b4['text'] == 'X' and self.b5['text'] == 'X' and self.b6['text'] == 'X' or
    		    self.b7['text'] == 'X' and self.b8['text'] == 'X' and self.b9['text'] == 'X' or
    		    self.b1['text'] == 'X' and self.b5['text'] == 'X' and self.b9['text'] == 'X' or
    		    self.b3['text'] == 'X' and self.b5['text'] == 'X' and self.b7['text'] == 'X' or
    		    self.b1['text'] == 'X' and self.b4['text'] == 'X' and self.b7['text'] == 'X' or
    		    self.b2['text'] == 'X' and self.b5['text'] == 'X' and self.b8['text'] == 'X' or
    		    self.b3['text'] == 'X' and self.b6['text'] == 'X' and self.b9['text'] == 'X'):
    			self.disable_button()
    			tkinter.messagebox.showinfo("Tic-Tac-Toe", 'X wins!')
    		
    		elif(self.flag==8):
    			self.disable_button()
    			tkinter.messagebox.showinfo("Tic-Tac-Toe", 'It\'s a tie!')
    
    		if (self.b1['text'] == 'O' and self.b2['text'] == 'O' and self.b3['text'] == 'O' or
    		    self.b4['text'] == 'O' and self.b5['text'] == 'O' and self.b6['text'] == 'O' or
    		    self.b7['text'] == 'O' and self.b8['text'] == 'O' and self.b9['text'] == 'O' or
    		    self.b1['text'] == 'O' and self.b5['text'] == 'O' and self.b9['text'] == 'O' or
    		    self.b3['text'] == 'O' and self.b5['text'] == 'O' and self.b7['text'] == 'O' or
    		    self.b1['text'] == 'O' and self.b4['text'] == 'O' and self.b7['text'] == 'O' or
    		    self.b2['text'] == 'O' and self.b5['text'] == 'O' and self.b8['text'] == 'O' or
    		    self.b3['text'] == 'O' and self.b6['text'] == 'O' and self.b9['text'] == 'O'):
    			self.disable_button()
    			tkinter.messagebox.showinfo("Tic-Tac-Toe", 'O wins!')
    
    	def click(self, button):
    		if button['text'] == '' and self.bclick == True:
    			button['text'] = 'X'
    			self.bclick=False
    			self.check_victory()
    			self.flag+=1
    
    		elif button['text'] == '' and self.bclick == False:
    			button['text'] = 'O'
    			self.bclick=True
    			self.check_victory()
    			self.flag+=1
    		
    		else:
    			tkinter.messagebox.showinfo("Tic-Tac-Toe", "Button already clicked!")
    
    
    	def disable_button(self):
    		self.b1.configure(state=DISABLED)
    		self.b2.configure(state=DISABLED)
    		self.b3.configure(state=DISABLED)
    		self.b4.configure(state=DISABLED)
    		self.b5.configure(state=DISABLED)
    		self.b6.configure(state=DISABLED)
    		self.b7.configure(state=DISABLED)
    		self.b8.configure(state=DISABLED)
    		self.b9.configure(state=DISABLED)
    
    
    TicTacToe(tic)
    tic.mainloop()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

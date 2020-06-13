---
title: tic_tac_toe
date: 2020-05-07
---
Example Python program tic_tac_toe.py

## Modules

* import tkinter

## Classes

* class Game(object):

## Methods

* def __init__(self):
* def check_win(self):
* def move(self, i):
* def check_full(self):
* def make_button_clicked(btn, i):
* def button_clicked():

## Code

Python tkinter example

    
    import tkinter
    
    
    master = tkinter.Tk()
    master.title('T-T-T')
    
    frame = tkinter.Frame(master)
    frame.grid()
    
    
    class Game(object):
        winners = [
            [0, 1, 2],
            [3, 4, 5],
            [6, 7, 8],
            [0, 3, 6],
            [1, 4, 7],
            [2, 5, 8],
            [0, 4, 8],
            [2, 4, 6],
            ]
        next_move = 'X'
        won = None
    
        def __init__(self):
            self.cells = [None] * 9
    
        def check_win(self):
            for winning in self.winners:
                one, two, three = winning
                if self.cells[one] == self.cells[two] and self.cells[two] == self.cells[three]:
                    if self.cells[one]:
                        self.won = self.cells[one]
            return self.won
    
        def move(self, i):
            if self.next_move:
                self.cells[i] = self.next_move
                if self.check_win() or self.check_full():
                    self.next_move = None
                else:
                    self.next_move = 'X' if self.next_move == 'O' else 'O'
            return self.cells[i]
    
        def check_full(self):
            for x in self.cells:
                if not x:
                    return False
            return True
    
    
    game = Game()
    
    
    def make_button_clicked(btn, i):
        def button_clicked():
            btn['text'] = game.move(i)
            if game.won:
                txt = game.won + ' won'
            elif game.next_move:
                txt = game.next_move + ' to move'
            else:
                txt = 'A draw!'
            lbl['text'] = txt
        return button_clicked
    
    
    for i in range(len(game.cells)):
        btn = tkinter.Button(frame, width=2, height=1, font=("Courier", 44))
        btn['command'] = make_button_clicked(btn, i)
        btn.grid(row=i//3, column=i % 3)
    
    
    lbl = tkinter.Label(master, text=game.next_move + ' to move', font=("Courier", 22))
    lbl.grid(row=1)
    
    tkinter.mainloop()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

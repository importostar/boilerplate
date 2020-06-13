---
title: mileston_project1
date: 2020-05-07
---
Example Python program mileston_project1.py
For Python version 2.x.
To test your Python version use:

    python --version

## Modules

* import os

## Methods

* def clear():
* def win_check():
* def tie():
* def replay():
* def header():
* def display(board):
* def game():

## Code

Python example

    #Your assignment: Create a Tic Tac Toe game. You are free to use any IDE you like.
    #Here are the requirements:
    #2 players should be able to play the game (both sitting at the same computer)
    #The board should be printed out every time a player makes a move
    #You should be able to accept input of the player position and then place a symbol on the board
    
    board = [" "," "," "," "," "," "," "," "," "," "];
    head = [0,1,2,3,4,5,6,7,8,9]
    win_comb = ((1,2,3),(4,5,6),(7,8,9),(1,4,7),(2,5,8),(3,6,9),(1,5,9),(3,5,7))
    
    import os
    
    def clear():
        os.system( 'cls' )
    
    def win_check():
        for a, b, c in win_comb:
            if board[a] == board[b] == board[c] == "X":
                print "PLAYER X IS THE WINNER!"
                return True
        for a, b, c in win_comb:
            if board[a] == board[b] == board[c] == "O":
                print "PLAYER O IS THE WINNER!"
                return True
    
    def tie():
        if board[1] != ' ' and board[2] != ' ' and board[3] != ' ' and board[4] != ' ' and board[5] != ' ' and board[6] != ' ' and board[7] != ' ' and board[8] != ' ' and board[9] != ' ':
            print "The game is a Tie"
            return True
    
    def replay():
        if win_check() == True or tie() == True:
            replay = raw_input(' Would you like to play again? \n y/n \n')
            if replay == 'y':
                return True
            if replay == 'n':
                print 'Goodbye'
                return False
    
    def header():
        print 'This is a game of Tic Tac Toe \n player X starts first then player O \n the aim of the game is to get 3 in a row. \n the game board looks like below, choose a number from 1 - 9 for your selection'
        print '|' + str(head[7]) + '|' + str(head[8]) + '|' + str(head[9]) + '|'
        print '-------'
        print '|' + str(head[4]) + '|' + str(head[5]) + '|' + str(head[6]) + '|'
        print '-------'
        print '|' + str(head[1]) + '|' + str(head[2]) + '|' + str(head[3]) + '|'
        print '-------'
    
    def display(board):
        print '|' + str(board[7]) + '|' + str(board[8]) + '|' + str(board[9]) + '|'
        print '-------'
        print '|' + str(board[4]) + '|' + str(board[5]) + '|' + str(board[6]) + '|'
        print '-------'
        print '|' + str(board[1]) + '|' + str(board[2]) + '|' + str(board[3]) + '|'
        print '-------'
    
    header()
    
    def game():
    
        while True:
    
            p_1 = raw_input("place an X on board position 1 to 9 \n")
            p_1 = int(p_1)
    
            if board[p_1] != 'X' and board[p_1] != 'O':
                board[p_1] = 'X'
            else:
                print ' \n This spot is taken \n '
            clear()
            display(board)
            if win_check() == True:
                if replay() == False:
                    break
            if tie() == True:
                if replay() == False:
                    break
    
            p_2 = raw_input("place an O on board position 1 to 9 \n")
            p_2 = int(p_2)
    
            if board[p_2] != 'O' and board[p_2] != 'X':
                board[p_2] = 'O'
            else:
                print 'This spot is taken \n'
    
            clear()
            display(board)
            if win_check() == True:
                if replay() == False:
                    break
            if tie() == True:
                if replay() == False:
                    break
    
    game()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

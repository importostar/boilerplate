---
title: Hangman
date: 2020-05-07
---
Example Python program Hangman.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import random as rd
* import numpy as np 

## Code

Python example

    # Hangman Game
    import random as rd
    import numpy as np 
    
    # choose the words
    word = ["tennis", "basketball", "baseball", "softball", "volleyball", "track", "football", "soccer", "golf", "cricket", "rugby", "lacrosse", "badminton", "bowling", "boxing", "hockey", "swimming", "archery", "fencing", "ultimate"]
    play = raw_input("Do you want to play the game? Answer Yes or No")
    while play == "Yes" or play == "yes" or play == " Yes" or play == " yes": #as long as person wants to play the game
    	word1 = rd.choice(word) # this is the word they are guessing
    	word2 = " "
    	count = 0
    	while word2 != word1:
    		while count <= 10:
    			letter = raw_input("What letter do you guess? ")
    			if letter in word1:
    				print("Yes that letter is in the word. ")
    				word2 = raw_input("Do you know the word? Type it here if you do or type anything else. ")
    				if word2 == word1:
    					print("You win!")
    					play = raw_input("Play again?")
    					break
    			else: 
    				print("Sorry that letter is not in the word. ")
    				count = count + 1
    				word2 = raw_input("Do you know the word? Type it here if you do or type anything else. ")
    				if word2 == word1:
    					print("You win!")
    					play = raw_input("Play again?")
    					break
    			if count == 10:
    				word2 = raw_input("You're out of guesses. You have one try to guess the word. ")
    				if word2 == word1:
    					print("You win!")
    					play = raw_input("Play again?")
    					break
    
    
    
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

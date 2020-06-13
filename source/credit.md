---
title: credit
date: 2020-05-07
---
Example Python program credit.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* from cs50 import get_int

## Code

Python example

    from cs50 import get_int
    
    while True:
        c = get_int("Enter your card : \n")
        digits = c  # storing a copy of the card to extract digits from
        nDigits = 0  # counting the digits in the card
        first = 0  # to store every individual digit, eventually storing the first digit of the card 
        second = 0  # stores the second digit
        s1 = 0  # sum of every 2nd digit from the end
        s = 0  # sum of every alternating digits starting from the end
        while digits > 0:   # while loop to go digit by digit and follow the algorithm
            second = first
            first = digits % 10
            digits = digits // 10
            
            if nDigits % 2 == 0:
                s = s + first
            else:
                temp = first * 2
                s1 = s1 + (temp % 10) + (temp // 10)
                
            nDigits += 1
            
        s2 = s1 + s
        firsttwo = first * 10 + second
        valid = s2 % 10 == 0  # stores a boolean value relative to the card being valid or not
        if (nDigits == 13 or nDigits == 16) and first == 4 and valid:
            print("VISA")
        elif nDigits == 15 and (firsttwo == 34 or firsttwo == 37) and valid:
            print("AMEX")
        elif firsttwo == 51 or firsttwo == 52 or firsttwo == 53 or firsttwo == 54 or firsttwo == 55 and nDigits == 16 and valid:
            print("MASTERCARD")
        else:
            print("INVALID")
        
        break

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

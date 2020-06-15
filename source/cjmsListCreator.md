---
title: cjmsListCreator
date: 2020-05-07
---
Example Python program cjmsListCreator.py
Python version 3.x or newer.
To check the Python version use:

    python --version


## Methods

* def main():
* def makeStrList(items):
* def addAccent(word):

## Code

Python example

    #Kyle Wright
    #This program will print a 2d list of strings
    #to be copied and pasted into the cjmsMimic program.
    #Therefore, this program only cuts down the time to create
    #a study set
    
    def main():
        list2 = []
        print("To add an accent or tilde, put a asterik(*)",
              "after the letter you wish to put an accent on.")
        for i in range(eval(input("Enter the number of vocab words: "))):
            list2.append(makeStrList(2))
        print(list2)
    
    def makeStrList(items):
        #Makes a list of specified length full of strings,
        #asking for an input each time
        list1 = []
        for i in range(items):
            iB = i == 0
            word = input("Enter the " + ("Spanish" if iB \
                               else "English") + " word in the list: ")
            if iB:
                for x in range(0, word.count("*")):
                    word = addAccent(word)
            list1.append(word)
        return list1
    
    def addAccent(word):
        letter = word[word.find("*") - 1]
        if letter == "a":
            letter = "á"
        elif letter == "e":
            letter = "é"
        elif letter == "i":
            letter = "í"
        elif letter == "o":
            letter = "ó"
        elif letter == "u":
            letter = "ú"
        elif letter == "n":
            letter = "ñ"
        word = word[0 : word.find("*") - 1] + letter + word[word.find("*") + 1 : ]
        return word
    main()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

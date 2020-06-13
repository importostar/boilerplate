---
title: Uncertanity (1)
date: 2020-05-07
---
Example Python program Uncertanity (1).py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import csv
* import sys
* import os
* import tkinter.filedialog
* import tkinter

## Methods

* def findNumbers(data):
* def user_input(folder):
* def find_file(folder):
* def find_root():
* def main():

## Code

Python tkinter example

    import csv
    import sys
    import os
    import tkinter.filedialog
    import tkinter
    
    
    def findNumbers(data):
        maxV = max(data)
        minV = min(data)
        avg = 0
        for i in range(len(data)):
            avg += data[i]
        avg = avg/len(data)
        uncertainty = max((maxV - avg), (avg-minV))
    
        print("The max value is: " + str(maxV))
        print("The min value is: " + str(minV))
        print("The average value is: " + str(avg))
    
        print("Max - Avg: " + str(maxV-avg))
        print("Avg - Min: " + str(avg-minV))
        print("The Uncertaninty is " + str(uncertainty))
    
    
    def user_input(folder):
        data = []
        outlier = -1
        fileIn = find_file(folder)
        csv_reader = csv.reader(fileIn, delimiter='\n')
        for item in csv_reader:
            data.append(item[0])
        fileIn.close()
        for i in range(len(data)):
            string = data[i]
            if(string[0] == "O"):
                outlier = i
            else:
                data[i] = float(data[i])
        if(outlier >= 0):
            string_outlier = data.pop(outlier)
            print("\nThere was an outlier, your outlier was " +
                  str(string_outlier[1:])+ "\n")
        return data
    
    
    def find_file(folder):
        fileExists = False
        user_quit = False
        fileName = input('Please enter a data file name: ')
        while fileExists == False:
            try:
                    fileIn = open(folder + "\\" + fileName, 'r')
                    fileExists = True
            except:
                fileName = input('An error occured trying to read the file.'
                                 + ' That file may not exist. Please try again: ')
    
        return fileIn
    
    def find_root():
        root = tkinter.Tk()
        root.withdraw()
        dirname = tkinter.filedialog.askdirectory(parent=root,initialdir="/",title='Please select a directory')
        return dirname
    
    def main():
        repeat = "Y"
        print("Type \"Quit\" at any time to stop the program")
        folder = find_root()
        while repeat.upper() == "Y":
            os.system('cls' if os.name == 'nt' else 'clear')
            data = user_input(folder)
            findNumbers(data)
            repeat = input("Do you have another CSV?(Y/N) ")
            
    
    
    main()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

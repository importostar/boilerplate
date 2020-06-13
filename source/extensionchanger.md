---
title: extensionchanger
date: 2020-05-07
---
Example Python program extensionchanger.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import os
* from os import listdir
* from os.path import isfile, join
* import pathlib
* import tkinter as tk
* from tkinter import filedialog

## Methods

* def main():
* def change():

## Code

Python tkinter example

    import os
    from os import listdir
    from os.path import isfile, join
    import pathlib
    import tkinter as tk
    from tkinter import filedialog
    
    def main():
        global onlyfiles
        global folderpath
        global filestarttype
        global fileendtype
        root = tk.Tk()
        root.withdraw()
    
        filename = filedialog.askdirectory()
    
        print(filename)
        folderpath = filename
        
        folderpath = os.path.abspath(folderpath)
        onlyfiles = [f for f in listdir(folderpath) if isfile(join(folderpath, f))]
        print(onlyfiles)
        
        cfiles = input("Are these the files you want to use? (y/N) ")
        if (cfiles == "y") or (cfiles == "Y"):
            filestarttype = input(
                "What file extension do you want to change? (default is .txt) ") or ".txt"
            fileendtype = input(
                "What file extension is the end result? (default is .bat) ") or ".bat"
            change()
        else:
            print("Restarting process")
            main()
    
            
    def change():
        global onlyfiles
    
        x = -2
        for i in onlyfiles:
            x = x+1
            if filestarttype in onlyfiles[x]:
                os.rename(os.path.join(folderpath, onlyfiles[x]), (os.path.join(
                    folderpath, onlyfiles[x].replace(filestarttype, fileendtype))))
    
        onlyfiles = [f for f in listdir(folderpath) if isfile(join(folderpath, f))]
        print("Done!")
        print(onlyfiles)
        input()
    
    if __name__ == "__main__":
        main()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

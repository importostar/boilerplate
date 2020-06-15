---
title: dna
date: 2020-05-07
---
Example Python program dna.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import sys
* import csv
* file = open(sys.argv[2], "r")  # importing the file contaning the sequence to be checked

## Methods

* def main():

## Code

Python example

    import sys
    import csv
    
    def main():
        if len(sys.argv) != 3:
            print("Usage: python dna.py data.csv sequence.txt")
            sys.exit(1)
    
        field = []  # stores the header(STRs)
        rows = []  # stores the data of each person read form the file
        with open(sys.argv[1], 'r') as csvfile:  # opening the databaes and copying the data into fields and rows
            csvreader = csv.reader(csvfile)
            fields = next(csvreader)
            for row in csvreader:
                rows.append(row)
    
        file = open(sys.argv[2], "r")  # importing the file contaning the sequence to be checked
        s = file.readline()  # stores the headers, (ex: 'name', 'agatc' etc..)
        i = 1  # running iteration through 1 since first column is not relecvant in checking for sequence match
        consec = []  # to store the consective matches in STRs
        while(i < len(fields)):
            j = 0
            max_result = 0
            a = 0  # temp variabe to store the count of matches in sequence
            while (j < len(s) - 1):  # checking for matches
                l = len(fields[i])
                if fields[i] == s[j:l + j]:
                    a += 1
                    j = j + l
                else:
                    if a > max_result:
                        max_result = a
                    a = 0
                    j = j + 1
            consec.append(max_result)  # stores result in an array for each STR
            i = i + 1
    
        # checking if the given sequence matches any from the database
        for k in rows:
            match = 0
            for j in k[1:]:
                for l in consec:
                    if int(j) == l:
                        match += 1
                        break
                if match == len(consec):
                    print(k[0])
                    exit(0)
    
        print("No match")
        exit(1)
    
    
    main()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

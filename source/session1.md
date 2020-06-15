---
title: session1
date: 2020-05-07
---
Example Python program session1.py
Python version 3.x or newer.
To check the Python version use:

    python --version


## Code

Python example

    #ich bin ein kommentar: dieselben Datenvariablen koennen bearbeitet werden, ausnahme true und false, python interpretiert true mit 1, false mit 0
    
    #integer
    
    z=2
    g=3
    
    print(z+g)
    
    #strings 2 strings koennen summiert werden
    x="fff"
    y="fffff"
    
    
    
    print(x+y)
    
    d=input("Enter your name here: ") #input() ist der befehl über console eingeben
    f="Hello "
    u="!"
    
    print(f+d+u)
    
    r=input("Gib mir eine Zahl: ")
    p=input("Gib mir eine Zahl: ")
    operator = input("Operator (+ oder -): ")
    
    r_als_zahl = int(r)
    p_als_zahl = int(p)
    
    # if+elif+else mehrere moeglichkeiten 
    
    if operator == "+":
        print(r_als_zahl+p_als_zahl)
    elif operator == "-":
        print(r_als_zahl-p_als_zahl)
    else:
        print("Der Operator ist ungueltig!")
    
    
    
    #print(r_als_zahl, p_als_zahl) mit beistrich koennen die einzelnen Werte nacheinander ausgegeben werden
    
    
    
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

---
title: databaseitemcounter
date: 2020-05-07
---
Example Python program databaseitemcounter.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import sqlite3

## Code

Python example

    import sqlite3
    
    conn = sqlite3.connect('emaildb.sqlite')
    cur = conn.cursor()
    
    cur.execute('DROP TABLE IF EXISTS Counts')
    
    cur.execute('''
    CREATE TABLE Counts (org TEXT, count INTEGER)''')
    
    fname = input('Enter file name: ')
    if (len(fname) < 1): fname = 'mbox-short.txt'
    fh = open(fname)
    for line in fh:
        if not line.startswith('From: '): continue
        pieces = line.split()
        email = pieces[1]
        email = email.split("@")
        email = email[1]
        cur.execute('SELECT count FROM Counts WHERE org = ? ', (email,))
        row = cur.fetchone()
        if row is None:
            cur.execute('''INSERT INTO Counts (org, count)
                    VALUES (?, 1)''', (email,))
        else:
            cur.execute('UPDATE Counts SET count = count + 1 WHERE org = ?',
                        (email,))
        conn.commit()
    
    # https://www.sqlite.org/lang_select.html
    sqlstr = 'SELECT org, count FROM Counts ORDER BY count DESC LIMIT 10'
    
    for row in cur.execute(sqlstr):
        print(str(row[0]), row[1])
    
    cur.close()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

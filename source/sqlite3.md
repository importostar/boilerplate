---
title: sqlite3
date: 2020-05-07
---
Example Python program sqlite3.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import sqlite3

## Methods

* def db_init():
* def db_write(tag, num, status):
* def db_read(key, filter_value):
*   def db_delete_tag(key):

## Code

Python example

    import sqlite3
    
    DB_FILE = 'database.db'
    
    def db_init():
        """
        Initialize the sqlite3 database if it doesn't exist or the tables are
        missing..
        :return: n/a
        """
        conn = sqlite3.connect(DB_FILE)
        c = conn.cursor()
    
        c.execute(
                'CREATE TABLE if not exists results \
                (tag text, num integer, status text')
        
        conn.commit()
        conn.close()
    
    def db_write(tag, num, status):
        global DEBUG
        """
        Writes results from a single boot to the database.
        :param data: Data to write.
        :param boot: Boot count.
        :return: n/a
        """
        conn = sqlite3.connect(DB_FILE)
        c = conn.cursor()
    
        row = (tag, num, status)
    
        c.execute('INSERT INTO results VALUES (?, ?, ?)', row)
        conn.commit()
        conn.close()
        
    def db_read(key, filter_value):
        if not os.path.isfile(DB_FILE):
          print('No db file detected!')
          exit()
            
        conn = sqlite3.connect(DB_FILE)
        conn.row_factory = sqlite3.Row
    
        c = conn.cursor()
    
        cmd = 'SELECT * FROM results'
        if key != '':
          cmd = cmd + ' WHERE tag = \"%s\" ' % key
          
        try:
            c.execute(cmd)
        except sqlite3.OperationalError:
            print cmd
        tbl = from_db_cursor(c)
        print(tbl)
        
        conn.close()
        
      def db_delete_tag(key):
          conn = sqlite3.connect(DB_FILE)
          conn.row_factory = sqlite3.Row
          c = conn.cursor()
      
          if DEBUG: print('Deleting %s from database' % key)
          c.execute('DELETE FROM results WHERE tag = \'%s\'' % key)
      
          conn.commit()
          conn.close()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

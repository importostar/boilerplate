---
title: db
date: 2020-05-07
---
Example Python program db.py

## Modules

* import psycopg2
* import sqlite3

## Classes

* class DB:

## Methods

* def __init__(self, filepath):
* def dump(self):
* def insert(self, tablename, **kwargs):
* def mktable(self, tablename, *args):
* def update(self, key, column, content):
* def remove(self, tablename, pred):

## Code

Python example

    import psycopg2
    
    dsn = dict(
    	dbname='dbname',
    	host='hostname',
    	password='password',
    	port=5432,
    	user='username'
    )
    conn = psycopg2.connect(**dsn)
    cursor = conn.cursor()
    cursor.execute('SELECT * FROM some-db')
    rows = cursor.fetchall()
    
    # -----------
    
    import sqlite3
    
    class DB:
        def __init__(self, filepath):
            self.filename = file_path
            self.connection = sqlite3.connect(filepath)
            self.cursor = self.connection.cursor()
        def dump(self):
            sql = 'SELECT * FROM records'
            self.cursor.execute(sql)
            return self.cursor.fetchall()
        def insert(self, tablename, **kwargs):
            sql = 'INSERT INTO {} ({}) VALUES({})'.format(tablename, kwargs.keys(), kwargs.values())
            self.cursor.execute(sql)
            self.connection.commit()
        def mktable(self, tablename, *args):
            self.cursor.execute('CREATE TABLE IF NOT EXISTS {} ({})').format(tablename, *args)
        def update(self, key, column, content):
            sql = """UPDATE records SET {}='{}' WHERE key={}""".format(column, content, key)
            self.cursor.execute(sql)
            self.connection.commit()
        def remove(self, tablename, pred):
            sql = 'DELETE FROM {} WHERE {}'.format(tablename, pred)
            self.cursor.execute(sql)
            self.connection.commit()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

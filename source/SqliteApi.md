---
title: SqliteApi
date: 2020-05-07
---
Example Python program SqliteApi.py
Python version 3.x or newer.
To check the Python version use:

    python --version


## Classes

* class SqlideApi():

## Methods

* def __init__(self, dbname, tablename):
* def millis(self):
* def connect(self):
* def add_data(self, barcode, task, executable, data):
* def getdata(self,barcode):

## Code

Python example

    tablenamen = 'barcodeTable'
    dbname = 'BarNote.db'
    
    class SqlideApi():
        def __init__(self, dbname, tablename):
            self.tablename = tablename
            self.dbname = dbname
            self.con = None
            try:
                self.con = lite.connect(self.dbname)
                with self.con:
                    cur = self.con.cursor()
                    cur.execute(
                        "CREATE TABLE IF NOT EXISTS " + tablename + "(barcode TEXT PRIMARY KEY NOT NULL, task TEXT,executable TEXT,data TEXT, time TEXT)")
                    print("Db initiated")
            except Exception as e:
                print(e)
                pass
            finally:
                if self.con:
                    self.con.close()
    
        def millis(self):
            return int(round(time_.time() * 1000))
    
        def connect(self):
            self.con = None
            try:
                self.con = lite.connect(self.dbname)
            except:
                pass
    
        def add_data(self, barcode, task, executable, data):
            self.connect()
            noterr = -1
            if self.con == None:
                print("Db connection error!")
                noterr = -1
                return  0
            mili = str(self.millis())
            cur = self.con.cursor()
            try:
                print("Trying to added data")
                cur.execute(
                    "INSERT INTO " + self.tablename + " (barcode,task,executable,data,time) VALUES('" + barcode + "','" + task + "','" + executable + "','" + data + "','" + mili + "')")
                self.con.commit()
                print("Added data")
                noterr = 1
            except Exception as e:
                try:
                    ex = "UPDATE " + self.tablename + " set task = ? ,executable = ? ,data = ? ,time = ? where barcode = ?"
                    cur.execute(ex, (task, executable, data, mili, barcode))
                    #cur.execute(ex, (task+"sfsf", executable+"sadasdsad", data+"adasdsad", mili+"asdsaddad", barcode))
                    self.con.commit()
                    noterr = 1
                except Exception as f:
                    print("Error in adding data")
                    noterr = -1
                    pass
                finally:
                    if self.con:
                        self.con.close()
            finally:
                if self.con:
                    self.con.close()
            return noterr
        def getdata(self,barcode):
            self.connect()
            if self.con == None:
                print("Db connection error!")
                eg.plugins.EventGhost.ShowOSD(u'Db connection error!', u'0;-24;0;0;0;700;0;0;0;1;0;0;2;32;Arial', (255, 255, 255),
                                              (0, 0, 0), 0, (0, 0), 0, 3.0, None)
                return False
            cur = self.con.cursor()
            cur.execute("SELECT * FROM "+self.tablename+" WHERE barcode=:barcode", {"barcode": barcode})
            row = cur.fetchone()
            self.con.close()
            return row
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

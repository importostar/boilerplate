---
title: MysqlUtil
date: 2020-05-07
---
Example Python program MysqlUtil.py

## Modules

* import MySQLdb

## Methods

* def get_mysqldb_conn():
* def get_page_index(item_count):
* def get_count_by_condition(conn, sql):
* def get_page_result(start, end, sql, conn):

## Code

Python example

    # -*- coding: utf-8 -*-
    import MySQLdb
    
    DB_SERVER_IP = '*.*.*.*'
    DB_PORT = 3306
    DB = '***'
    
    DB_USERNAME = 'root'
    DB_PASSWORD = '******'
    
    def get_mysqldb_conn():
        conn = MySQLdb.connect(
            host=DB_SERVER_IP,
            port=DB_PORT,
            user=DB_USERNAME,
            passwd=DB_PASSWORD,
            db=DB,
            charset='utf8'
        )
        return conn
    
    
    def get_page_index(item_count):
        L = range(item_count)
        L_index = L[::100]
        # 分页:0,100,200,...,max
        L_index.append(item_count)
        return L_index
    
    
    def get_count_by_condition(conn, sql):
        cursor = conn.cursor()
        cursor.execute(sql)
        count = cursor.fetchall()
        cursor.close()
        return count[0][0]
    
    
    def get_page_result(start, end, sql, conn):
        cursor = conn.cursor()
        end_fix = "limit %d,%d" % (start, end)
        new_sql = sql + " " +  end_fix
        cursor.execute(new_sql)
        data = cursor.fetchall()
        cursor.close()
        return data
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

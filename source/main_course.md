---
title: main_course
date: 2020-05-07
---
Example Python program main_course.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import pymysql.cursors
* import commands
* import os
* import re

## Methods

* def select_items():
* def select_second(items):
* def read_time(items):
* def print_sql(items):

## Code

Python example

    #! /usr/bin/python
    #-*- coding: utf-8 -*-
    
    # 1 查数据库 返回数据
    # 2 根据url 和本地ffmpeg查询时长
    # 3 输出更新的sql语句
    
    import pymysql.cursors
    import commands
    import os
    import re
    
    site = 'https://zxycdn.zhixueyun.com/'
    
    connection = pymysql.connect(host='xxx',
                                 user='devuser',
                                 password='xxx',
                                 db='course-study',
                                 charset='utf8mb4',
                                 cursorclass=pymysql.cursors.DictCursor)
    def select_items():
        with connection.cursor() as cursor:
            sql = '''
            select  t_course_chapter_section.f_id as 'sectionId',
            t_course_chapter_section.`f_attachment_id` as 'attachmentId'
            from t_course_chapter_section 
            left join t_course_info on t_course_info.f_id = t_course_chapter_section.f_course_id
            where (f_time_second = 0 or f_time_second is null)  and (f_time_minute = 0 or f_time_minute is null)
            and f_section_type in (5,6)
            and t_course_info.f_delete_flag <>1
            order by t_course_info.f_create_time desc;
            '''
            cursor.execute(sql)
            return cursor.fetchall()
    
    def select_second(items):
        sql = '''
            select f_path from `human-resource`.`t_attachment` where f_id = '%s';
            '''
        with connection.cursor() as cursor:
            for item in items:
                cursor.execute(sql % (item['attachmentId'],))
                item['path'] = cursor.fetchone()['f_path']
    
    def read_time(items):
        for item in items:
            url = site + item['path']
            print('send url %s'%(url,))
            cmd = 'ffprobe ' + url
            (err_code, text) = commands.getstatusoutput(cmd)
            duration = r'(\d\d):(\d\d):(\d\d).(\d+)'
            (h, t, s, m) = re.search(duration, text).groups()
            second= (int(h)*60*60 + int(t)*60 + int(s))
            item['second'] = second
            # print m.group(1)
    
    def print_sql(items):
        with open('update_second_course.sql','w') as f:
            for item in items:
                text = "update `course-study`.t_course_chapter_section set f_time_second = %s where f_id = '%s';" %(item['second'], item['sectionId'])
                print(text)
                print >> f, text
    
    if __name__ == '__main__':
        items = select_items()
        select_second(items)
        read_time(items)
        print_sql(items)

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

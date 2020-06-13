---
title: lambda_function general
date: 2020-05-07
---
Example Python program lambda_function-general.py
For Python version 2.x.
To test your Python version use:

    python --version

## Modules

* import datetime
* import time
* import boto3

## Methods

* def get_from_timestamp():
* def get_to_timestamp(from_ts):
* def lambda_handler(event, context):

## Code

Python example

    import datetime
    import time
    import boto3
    
    log_name_general = 'general-log'
    log_group_name_general = '/aws/rds/cluster/xxxxx/general'
    s3_bucket_name = 'xxxxxxxxxx'
    s3_prefix_general = 'xxxx/log/mysql/' + log_name_general + '/%s' % (datetime.date.today().strftime("%Y")) + '/%s' % (datetime.date.today().strftime("%m")) + '/%s' % (datetime.date.today().strftime("%d"))
    
    def get_from_timestamp():
        #now = datetime.date.today()
        today = datetime.date.today()
        yesterday = datetime.datetime.combine(today - datetime.timedelta(days = 1), datetime.time(0, 0, 0))
        #today = datetime.datetime.combine(now, datetime.time(0, 0, 0))
        timestamp = time.mktime(yesterday.timetuple())
        #timestamp = time.mktime(now.timetuple())
        return int(timestamp)
    
    def get_to_timestamp(from_ts):
        return from_ts + (60 * 60 * 24) - 1
    
    def lambda_handler(event, context):
        from_ts = get_from_timestamp()
        to_ts = get_to_timestamp(from_ts)
        print 'Timestamp: from_ts %s, to_ts %s' % (from_ts, to_ts)
    
        client = boto3.client('logs')
        
        response = client.create_export_task(
            logGroupName      = log_group_name_general,
            fromTime          = from_ts * 1000,
            to                = to_ts * 1000,
            destination       = s3_bucket_name,
            destinationPrefix = s3_prefix_general
        )
        return response

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

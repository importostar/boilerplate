---
title: kinesis
date: 2020-05-07
---
Example Python program kinesis.py

## Modules

* import boto3
* import json

## Classes

* class SensorEvent(object):

## Methods

*  def __init__(self, sensorId, data):

## Code

Python example

    # http://boto3.readthedocs.io/en/latest/reference/services/kinesis.html
    import boto3
    import json
    
    client = boto3.client('kinesis')
    
    create_stream = client.create_stream(StreamName='GregorSamsa', ShardCount=150)
    
    streams = client.list_streams(Limit=100)
    
    class SensorEvent(object):
         def __init__(self, sensorId, data):
            self.sensorId = sensorId
            self.data = data
    
    for sensorEvent in [SensorEvent("1", "something happened"), SensorEvent("2", "something again happened")]:
         client.put_record(StreamName='GregorSamsa', Data=json.dumps(sensorEvent.__dict__), PartitionKey=sensorEvent.sensorId)
         
    toInt(MD5 of 1) = 261578874264819908609102035485573088411
    
    #{'SequenceNumber': '49574391176947112863656757427907696591655425940803028786', 'ResponseMetadata': {'HTTPHeaders': {'content-length': '110', 'x-amzn-requestid': 'fd00a7f5-39e1-20f6-acc5-a59bd6ca5be1', 'content-type': 'application/x-amz-json-1.1', 'server': 'Apache-Coyote/1.1', 'date': 'Wed, 21 Jun 2017 23:24:30 GMT', 'x-amz-id-2': 'JYuozovloYQiCyXDxAhmTTY29AHhGIlqiC2zGsj/svtCck2nDe/HS785SY0vdr4OuvGvL4dTwxCvRfMLuv9Wa0YfdJ2n4NUZ'}, 'RetryAttempts': 0, 'RequestId': 'fd00a7f5-39e1-20f6-acc5-a59bd6ca5be1', 'HTTPStatusCode': 200}, 'ShardId': 'shardId-000000000115'}
    #{'SequenceNumber': '49574391176991714354053818674191976954020337292989695826', 'ResponseMetadata': {'HTTPHeaders': {'content-length': '110', 'x-amzn-requestid': 'e376b52e-772f-e5d3-b2b3-b74098049ec4', 'content-type': 'application/x-amz-json-1.1', 'server': 'Apache-Coyote/1.1', 'date': 'Wed, 21 Jun 2017 23:24:30 GMT', 'x-amz-id-2': 'C75YgF1cKYIgQc1lSYZvmsdDvPhc+71qDAacRjFGbAtMpTLdZaENtK9lGew0pc09ZiSkfRG5raOHXLNTItyfSBPomKCc/Vnp'}, 'RetryAttempts': 0, 'RequestId': 'e376b52e-772f-e5d3-b2b3-b74098049ec4', 'HTTPStatusCode': 200}, 'ShardId': 'shardId-000000000117'}
    
    cursor = client.get_shard_iterator(StreamName='GregorSamsa', , ShardId='shardId-00000', ShardIteratorType='TRIM_HORIZON')
    
    client.get_records( ShardIterator=cursor["ShardIterator"], Limit=10000)
    
    #
    # {'Records': [{'PartitionKey': '1', 'ApproximateArrivalTimestamp': datetime.datetime(2017, 6, 21, 23, 24, 30, 661000, tzinfo=tzlocal()), 'SequenceNumber': '49574391176947112863656757427907696591655425940803028786', 'Data': b'{"data": "something happened", "sensorId": "1"}'}], 'MillisBehindLatest': 0, 'NextShardIterator': 'AAAAAAAAAAHq8axv9lHphjtFpGis3xnexFn73/whruqLDnFR55xjUXleyM4Ci/i0hSld6ISzMb51xUoYkV2EHsjQCBtfNn74Gc25yrIVLZ5kH4VLxf64Q4gCgK3ABJxBTuXThv+UVA+iklVjObroqLE3tUMBke2bpciQp+fnzn4SLs9dARPsZHKqDtR0CZxddAT4HoMQhhUx1clOR81jbaWabyzBY6bG', 'ResponseMetadata': {'HTTPHeaders': {'content-length': '501', 'x-amzn-requestid': 'c87d168f-8704-d00c-99b8-10d42eb35d3e', 'content-type': 'application/x-amz-json-1.1', 'server': 'Apache-Coyote/1.1', 'date': 'Wed, 21 Jun 2017 23:41:15 GMT', 'x-amz-id-2': 'Gmy8eZ4nXfu6tb0WkVvY20AlXnev7L8OIPRvTZDF07EFGlYYpHzWvxvOXRDnIUkX1vx9+QYaUXi6SdoUx7QEUsr7N90RVk7G'}, 'RetryAttempts': 0, 'RequestId': 'c87d168f-8704-d00c-99b8-10d42eb35d3e', 'HTTPStatusCode': 200}}
    #

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

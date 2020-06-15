---
title: boto3 (1)
date: 2020-05-07
---
Example Python program boto3 (1).py

## Modules

* import ecshelper
* import boto3
* import ecshelper
* import boto3

## Code

Python example

    mylaptop:cleverfolder mycleverusername$ python cleverfile.py
    Traceback (most recent call last):
      File "cleverfile.py", line 3, in <module>
        import ecshelper
      File "/Users/mycleverusername/Documents/git.sabre.com/cleverfolder/ecshelper.py", line 3, in <module>
        import boto3
    ImportError: No module named boto3
      
    mylaptop:cleverfolder mycleverusername$ pip install boto3
    Requirement already satisfied: boto3 in /usr/local/lib/python2.7/site-packages (1.7.62)
    Requirement already satisfied: jmespath<1.0.0,>=0.7.1 in /Users/mycleverusername/Library/Python/2.7/lib/python/site-packages (from boto3) (0.9.3)
    Requirement already satisfied: s3transfer<0.2.0,>=0.1.10 in /Users/mycleverusername/Library/Python/2.7/lib/python/site-packages (from boto3) (0.1.13)
    Requirement already satisfied: botocore<1.11.0,>=1.10.62 in /usr/local/lib/python2.7/site-packages (from boto3) (1.10.62)
    Requirement already satisfied: futures<4.0.0,>=2.2.0; python_version == "2.6" or python_version == "2.7" in /Users/mycleverusername/Library/Python/2.7/lib/python/site-packages (from s3transfer<0.2.0,>=0.1.10->boto3) (3.2.0)
    Requirement already satisfied: docutils>=0.10 in /Users/mycleverusername/Library/Python/2.7/lib/python/site-packages (from botocore<1.11.0,>=1.10.62->boto3) (0.14)
    Requirement already satisfied: python-dateutil<3.0.0,>=2.1; python_version >= "2.7" in /Users/mycleverusername/Library/Python/2.7/lib/python/site-packages (from botocore<1.11.0,>=1.10.62->boto3) (2.7.2)
    Requirement already satisfied: six>=1.5 in /usr/local/lib/python2.7/site-packages (from python-dateutil<3.0.0,>=2.1; python_version >= "2.7"->botocore<1.11.0,>=1.10.62->boto3) (1.11.0)
    
    mylaptop:cleverfolder mycleverusername$ python cleverfile.py
    Traceback (most recent call last):
      File "cleverfile.py", line 3, in <module>
        import ecshelper
      File "/Users/mycleverusername/Documents/git.sabre.com/cleverfolder/ecshelper.py", line 3, in <module>
        import boto3
    ImportError: No module named boto3

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

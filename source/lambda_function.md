---
title: lambda_function
date: 2020-05-07
---
Example Python program lambda_function.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import os
* import requests

## Methods

* def get_host():
* def authn_webapp(event):
* def lambda_handler(event, context):

## Code

Python example

    import os
    import requests
    
    
    def get_host():
        tld = 'stage.example.com'
        host = f'https://{tld}'
    
        webapp_stage_user = os.environ["STAGE_USN"]
        webapp_stage_pass = os.environ["STAGE_PSW"]
    
        creds = f'{webapp_stage_user}:{webapp_stage_pass}'
        host = f'https://{creds}@{tld}'
    
        return host
    
    
    def authn_webapp(event):
        data = {'username': event['userName'],
                'password': event['request']['password']}
    
        uri = f'{get_host()}/api/login'
    
        return requests.post(uri, data=data)
    
    
    def lambda_handler(event, context):
        """
        There are two states:
    
        1. authentication (but before user created in cognito)
        2. forgotten password
    
        For authentication we log the user into our webapp and then extract their
        details and modify the user account that is about to be created in cognito.
        
        This allows us to handle migrating users from our data store to cognito.
        """
        if event['triggerSource'] == "UserMigration_Authentication":
            login_response = authn_webapp(event)
    
            if login_response.status_code == 200:
                d = login_response.json()
    
                user_attr = {'username': d['username'],
                             'name': d['display_name'],
                             'email': d['email'],
                             'email_verified': 'true',
                             'custom:webapp_id': d['userid']}
    
                event['response']['userAttributes'] = user_attr
                event['response']['finalUserStatus'] = "CONFIRMED"
                event['response']['messageAction'] = "SUPPRESS"
    
                return event
            else:
                return None
        else:
            return None
    
    
    if __name__ == "__main__":
        event = {'triggerSource': 'UserMigration_Authentication',
                 'userName': 'beep',
                 'request': {'password': 'boop'},
                 'response': {}}
    
        result = lambda_handler(event, {})
    
        print(f'result: {result}')
    
    # Build package:
    #   make build
    #       pipenv run pip install -r <(pipenv lock -r) --target ./
    #       zip -r lambda.zip ./
    #
    # Test locally:
    #   make run
    #       STAGE_USN=123 STAGE_PSW=456 python lambda_function.py

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

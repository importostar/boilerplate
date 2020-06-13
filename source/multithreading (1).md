---
title: multithreading (1)
date: 2020-05-07
---
Example Python program multithreading (1).py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import bottle
* import json
* import requests
* from threading import Thread

## Methods

* def postprocessed_handle():
* def process_data(data):
* def process_handle():

## Code

Python example

    #!/usr/bin/env python
    # -*- coding: utf-8 -*-
    
    """ Sample multithreading with bottle.py
    Requirements: requests, bottle
    
    To run: 
    $ python app.py
    
    To post data, open another command shell and type:
    $ curl -X POST -H "Content-Type: application/json" -d '{"data":"test"}' http://127.0.0.1:8080/process -D-
    
    """
    import bottle
    import json
    import requests
    from threading import Thread
    
    POSTBACK_URL = 'http://127.0.0.1:8080/postprocessed'
    
    @bottle.post('/postprocessed')
    def postprocessed_handle():
      print('Received data at postprocessed')
      return bottle.HTTPResponse(status=200, body="Complete postprocessed")
    
    def process_data(data):
      # do processing...
      result = json.dumps(data)
    
      print('Finished processing')
      requests.post(POSTBACK_URL, data=result, 
        headers={'Content-Type':'application/json'})
                   
    @bottle.post('/process')
    def process_handle():
      data = bottle.request.json.get('data', False)
      print('Received data at process: ' + data)
    
      if not data:
        return bottle.HTTPResponse(status=400, body="Missing data")
    
      #Spawn thread to process the data
      t = Thread(target=process_data, args=(data, ))
      t.start()
    
      #Immediately return a 200 response to the caller
      return bottle.HTTPResponse(status=200, body="Complete process")
    
    if __name__ == '__main__':
      bottle.run()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

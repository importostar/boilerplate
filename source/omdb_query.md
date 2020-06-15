---
title: omdb_query
date: 2020-05-07
---
Example Python program omdb_query.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import requests
* import json

## Code

Python example

    # Query OMDB using an api and my api key
    # Created By David J Pearson, April 2019
    # Version 1.0
    # ------------------------------------------
    
    import requests
    import json
    
    # Setup OMDB api key token and base url
    
    api_token = 'i=tt3896198&apikey=74fcb169'
    api_url_base = 'http://www.omdbapi.com/?'
    
    # Construct the actual url used in the GET action of the OMDB api
    
    myquery = str(input("Enter Movie Title: "))
    api_url = "{}{}&t={}".format(api_url_base, api_token, myquery)
    
    # Connect to OMDB and query using my url
    response = requests.get(api_url)
    
    if response.status_code == 200:
    
      # If connect to OMDB is ok, store response as a dictionary
      ans = json.loads(response.content.decode('utf-8'))
      
      # Test for dictionary key 'Error' to see if movie exists in OMDB
      if 'Error' in ans:
      	print(ans['Error'])
      else:
      
        # Movie exists so just print the dictionary
        print(ans) 
    else:
    
      # If my url is bad, so an error message
      print("Sorry - Not a valid request to OMDB")
            
    # ------- End of code -------------
    
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

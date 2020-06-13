---
title: zabbix_api_search_inven_notes
date: 2020-05-07
---
Example Python program zabbix_api_search_inven_notes.py
For Python version 2.x.
To test your Python version use:

    python --version

## Modules

* import os
* import sys
* import getpass
* import json
* import urllib2

## Code

Python example

    #!/usr/bin/python
    # coding: utf-8
    
    import os
    import sys
    import getpass
    import json
    import urllib2
    
    if len(sys.argv) != 2 :
      print ' ERROR : Please check Search hostname.'
      print '  Usage: ' + os.path.basename(__file__) + ' [search hostname]'
      sys.exit()
    
    client = 'https://127.0.0.1/zabbix/api_jsonrpc.php'
    postheader = {'Content-Type': 'application/json-rpc'}
    
    userid = raw_input('Please Enter Zabbix Web Account : ')
    passwd = getpass.getpass('PASSWORD :')
    while userid == '':
      print 'type the account.'
      userid = raw_input('Please Enter Zabbix Web Account : ')
    while passwd == '':
      print 'type the password'
      passwd = getpass.getpass('PASSWORD :')
    
    # auth
    authquery = json.dumps({'jsonrpc':'2.0', 'method':'user.login', 'params':{'user':userid, 'password':passwd}, 'auth':None, 'id': 1})
    authreq = urllib2.Request(client, authquery, postheader)
    
    try :
      getauthresult = urllib2.urlopen(authreq).read()
      authresult = json.loads(getauthresult)
    
    except Exception as e :
      print ' %s %s' % ('ERROR :',e)
      print '         Please check zabbix URL Setting or Others.'
      sys.exit()
    
    if 'error' in authresult :
      print ' %s %s' % ('API Error :',authresult['error']['data'])
      sys.exit()
    
    # query
    postquery = json.dumps({'jsonrpc':'2.0', 'method':'host.get', 'params':{'output':'extend', 'filter':{'status':'0', 'host':sys.argv[1]}, 'selectInventory':'extend'}, 'auth':authresult['result'], 'id':1})
    postreq = urllib2.Request(client, postquery, postheader)
    getpostresult = urllib2.urlopen(postreq).read()
    postresult = json.loads(getpostresult)
    
    # result is empty
    if not postresult['result'] :
      print 'no such host.'
      sys.exit()
    
    # result data export
    info=[]
    for data in postresult['result'] :
      if not data['inventory'] :
        print 'no such inventory .'
        sys.exit()
      info = data['inventory']['notes']
    
    print '--------------------------------------------------'
    print '%s%s%s%s%s' % ('# INFO ->  ', sys.argv[1], ' : ', '\n', info)
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

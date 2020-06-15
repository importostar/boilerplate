---
title: zabbix_api_get_all_hosts_ips
date: 2020-05-07
---
Example Python program zabbix_api_get_all_hosts_ips.py
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
    
    client = 'http://127.0.0.1/zabbix/api_jsonrpc.php'
    postheader = {'Content-Type': 'application/json-rpc'}
    
    userid = raw_input("Please Enter Zabbix Web Account : ")
    passwd = getpass.getpass('PASSWORD :')
    while userid == "":
      print "type the account."
      userid = raw_input("Please Enter Zabbix Web Account : ")
    while passwd == '':
      print 'type the password'
      passwd = getpass.getpass('PASSWORD :')
    
    # auth
    authquery = json.dumps({'jsonrpc':'2.0', 'method':'user.login', 'params':{'user':userid, 'password':passwd}, 'auth':None, 'id': 1})
    authreq = urllib2.Request(client, authquery, postheader)
    
    try :
      getauthresult = urllib2.urlopen(authreq).read()
      authresult = json.loads(getauthresult)
    #  print authresult['result']
    
    except :
      print " ERROR : Please check zabbix Account or Password."
      print "  Usage: " + os.path.basename(__file__) + " [search hostname]"
      sys.exit()
    
    # query
    postquery = json.dumps({'jsonrpc':'2.0', 'method':'host.get', 'params':{'output':'extend', 'selectInterfaces':'extend', 'filter':{'status':'0'}}, 'auth':authresult['result'], 'id':1})
    postreq = urllib2.Request(client, postquery, postheader)
    getpostresult = urllib2.urlopen(postreq).read()
    postresult = json.loads(getpostresult)
    #print postresult
    
    for data in postresult['result'] :
      host_name = data['host']
      ip_addr = data['interfaces'].keys()
      for ips in ip_addr:
          ip = data['interfaces'][ips]['ip']
      print '%s%s%s' % (host_name, '\t', ip)
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

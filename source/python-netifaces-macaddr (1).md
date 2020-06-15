---
title: python netifaces macaddr (1)
date: 2020-05-07
---
Example Python program python-netifaces-macaddr (1).py

## Modules

* >>> import netifaces
* import netifaces as nif

## Methods

* def mac_for_ip(ip):

## Code

Python example

    netifaces is a good module to use for getting the mac address (and other addresses). It's crossplatform and makes a bit more sense than using socket or uuid.
    
    >>> import netifaces
    >>> netifaces.interfaces()
    ['lo', 'eth0', 'tun2']
    
    >>> netifaces.ifaddresses('eth0')[netifaces.AF_LINK]
    [{'addr': '08:00:27:50:f2:51', 'broadcast': 'ff:ff:ff:ff:ff:ff'}]
    
    
    
    import netifaces as nif
    def mac_for_ip(ip):
        'Returns a list of MACs for interfaces that have given IP, returns None if not found'
        for i in nif.interfaces():
            addrs = nif.ifaddresses(i)
            try:
                if_mac = addrs[nif.AF_LINK][0]['addr']
                if_ip = addrs[nif.AF_INET][0]['addr']
            except IndexError, KeyError: #ignore ifaces that dont have MAC or IP
                if_mac = if_ip = None
            if if_ip == ip:
                return if_mac
        return None

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

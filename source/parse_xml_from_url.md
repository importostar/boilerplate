---
title: parse_xml_from_url
date: 2020-05-07
---
Example Python program parse_xml_from_url.py

## Modules

* #import library to do http requests:
* import urllib2
* #import easy to use xml parser called minidom:
* from xml.dom.minidom import parseString
* #all these imports are standard on most modern python implementations

## Code

Python example

    #import library to do http requests:
    import urllib2
     
    #import easy to use xml parser called minidom:
    from xml.dom.minidom import parseString
    #all these imports are standard on most modern python implementations
     
    #download the file:
    file = urllib2.urlopen('http://www.somedomain.com/somexmlfile.xml')
    #convert to string:
    data = file.read()
    #close file because we dont need it anymore:
    file.close()
    #parse the xml you downloaded
    dom = parseString(data)
    #retrieve the first xml tag (<tag>data</tag>) that the parser finds with name tagName:
    xmlTag = dom.getElementsByTagName('tagName')[0].toxml()
    #strip off the tag (<tag>data</tag>  --->   data):
    xmlData=xmlTag.replace('<tagName>','').replace('</tagName>','')
    #print out the xml tag and data in this format: <tag>data</tag>
    print xmlTag
    #just print the data
    print xmlData

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

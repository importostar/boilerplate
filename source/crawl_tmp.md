---
title: crawl_tmp
date: 2020-05-07
---
Example Python program crawl_tmp.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import urllib.request
* from bs4 import BeautifulSoup
* import re

## Code

Python example

    import urllib.request
    from bs4 import BeautifulSoup
    import re
    # for tag in soup.find_all(re.compile("^b")):
    #     print(tag.name)
    
    
    response = urllib.request.urlopen('http://www.recoveryversion.com.tw/gb/read_List.php?f_BookNo=1&f_ChapterNo=1&f_VerseNo=1')
    html = response.read().decode('UTF-8')
    #print (html)
    
    for line in html:
        if re.match(r'^(.*)',line):
            print (line)
    #Try use re first then use beautifulsoup.
    # pattern = re.compile(r"<td id=\"1\" width=\"56\">1:1</td>\n<td colspan=\"6\" width=\"468\">(.*)<tr>\n<td id=\"2\" width=\"56\">1:2</td>",re.MULTILINE|re.DOTALL)
    # for match in pattern.finditer(html):
    #     x = match.groups()
    #     tmp1=x[0]
    #     print (tmp1)
    #     for line in tmp1:
    #         if line.startswith('<span'):
        # soup = BeautifulSoup(x[0], "html5lib")
        # print(soup.find("td"))
    
    #Try use bs before use re:
    # soup = BeautifulSoup(html, "html5lib")
    #
    # print (soup.find (id="1").string)
    # soup.find("div", {"id": "1"})
    # tag=soup.div
    # print(tag.string)
    # soup = BeautifulSoup(html, "html5lib")
    # soup = BeautifulSoup('<b class="boldest">Extremely bold</b>')
    # print(soup.prettify())
    # soup.find("div", {"id": "1"})
    # print (soup.find (id="1"))
    
    # print (soup.find (id="1").string)

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

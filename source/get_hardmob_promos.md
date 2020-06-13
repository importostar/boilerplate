---
title: get_hardmob_promos
date: 2020-05-07
---
Example Python program get_hardmob_promos.py

## Modules

* import re
* import sys
* import time
* import requests
* import threading
* import Tkinter
* from BeautifulSoup import BeautifulSoup

## Methods

* def show_promo_window(size,promo):

## Code

Python tkinter example

    #!/usr/local/bin/python
    # -*- coding: utf-8 -*-
    
    import re
    import sys
    import time
    import requests
    import threading
    import Tkinter
    from BeautifulSoup import BeautifulSoup
    
    old_list = []
    print_first_time = 1
    
    def show_promo_window(size,promo):
    	root = Tkinter.Tk()
    	root.geometry('{}x50+1350+750'.format(size))
    	Tkinter.Label(root, text=promo).place(x=10, y=10)
    	threading.Timer(1.5, root.destroy).start() 
    	root.mainloop()
    
    while 1:
    	soup = BeautifulSoup(requests.get('http://www.hardmob.com.br/promocoes/?sort=lastpost&order=dsc').content)
    	h3_tags = soup.findAll('h3', { "class" : "threadtitle" } )
    	topics = [re.sub(',|\n|\r','',x) for x in re.split('\n\n',re.sub(r'<[^>]+>|\[|\]','',str(h3_tags)))[2:] if x != '']
    	print_topics = [i for i, j in zip(topics, old_list) if i != j]
    	if len(print_topics) != 0 or print_first_time == 1:
    		for topic in print_topics:
    			for word in sys.argv[1].split(','):
    				if word.upper() in topic.upper():
    					show_promo_window(len(topic)*7,topic)
    					break
    		if len(print_topics) != 0:
    			for x in print_topics:
    				print >> open('/home/kanazuchi/topics_promo','a'), x
    		elif print_first_time == 1:
    			for x in topics:
    				print >> open('/home/kanazuchi/topics_promo','a'), x
    				show_promo_window(len(x)*7,x)
    		print_topics = []
    	old_list = topics
    	print_first_time = 0
    	time.sleep(120)

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

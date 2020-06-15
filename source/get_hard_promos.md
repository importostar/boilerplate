---
title: get_hard_promos
date: 2020-05-07
---
Example Python program get_hard_promos.py

## Modules

* import re
* import sys
* import time
* import Tkinter
* import argparse
* import requests
* import threading
* from BeautifulSoup import BeautifulSoup

## Methods

* def set_parser():
* def show_promo_window(t,size,promo):

## Code

Python tkinter example

    #!/usr/local/bin/python
    # -*- coding: utf-8 -*-
    # @kanazuchi_ <kanazuchi@alvolivre.com>
    
    import re
    import sys
    import time
    import Tkinter
    import argparse
    import requests
    import threading
    from BeautifulSoup import BeautifulSoup
    
    def set_parser():
    	parser = argparse.ArgumentParser()
    	parser.add_argument(
    		'-f', dest='words_filter',
    		action='store',
    		default = 'all',
    		help='Entre com as palavras que deseja filtrar, default = all')
    	return parser.parse_args()
    
    def show_promo_window(t,size,promo):
    	root = Tkinter.Tk()
    	root.geometry('{}x45+1300+750'.format(size))
    	Tkinter.Label(root, text=promo).place(x=10, y=10)
    	threading.Timer(t, root.destroy).start()
    	root.mainloop()
    
    opts = set_parser()
    old_list = []
    print_first_time = 1
    
    while 1:
    	try:
    		soup = BeautifulSoup(requests.get('http://www.hardmob.com.br/promocoes/?sort=lastpost&order=desc').content)
    		h3_tags = soup.findAll('h3', { "class" : "threadtitle" } )
    		topics = [re.sub(',|\n|\r','',x) for x in re.split('\n\n',re.sub(r'<[^>]+>|\[|\]','',str(h3_tags)))[2:] if x != '']
    		print_topics = [i for i in topics if i not in [x for x in old_list]]
    		if len(print_topics) != 0:
    			if opts.words_filter != 'all':
    				for topic in print_topics:
    					for word in opts.words_filter.split(','):
    						if word.upper() in topic.upper():
    							show_promo_window(3,int(len(topic)*6.7),topic)
    							break
    			else:
    				for topic in print_topics:
    					show_promo_window(2,int(len(topic)*6.7),topic)
    		elif print_first_time == 1:
    			for topic in topics:
    				show_promo_window(0.5,int(len(x)*6.7),topic)
    		print_topics = []
    		old_list = topics
    		print_first_time = 0
    		time.sleep(60)
    	except:
    		pass

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

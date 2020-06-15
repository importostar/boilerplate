---
title: test
date: 2020-05-07
---
Example Python program test.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* from gi.repository import Gtk
* # from twitter import *
* # import os.path
* # import webbrowser

## Classes

* class MainWindow(Gtk.Window):
* class HelloWindow(Gtk.Window):

## Methods

* 	def __init__(self):
* 	def onclick(self, widget):
* 	def __init__(self):
* # def authenticate():

## Code

Python example

    #!/usr/bin/python
    from gi.repository import Gtk
    # from twitter import *
    # import os.path
    # import webbrowser
    
    class MainWindow(Gtk.Window):
    	def __init__(self):
    		Gtk.Window.__init__(self, title="Hello World")
    		self.button = Gtk.Button(label="Button")
    		self.button.connect("clicked", self.onclick)
    		self.add(self.button)
    
    	def onclick(self, widget):
    		new_win = HelloWindow()
    		new_win.show_all()
    
    
    class HelloWindow(Gtk.Window):
    	def __init__(self):
    		Gtk.Window.__init__(self)
    		self.label = Gtk.Label(label="Tweet!")
    		self.add(self.label)
    
    win = MainWindow()
    win.connect("delete-event", Gtk.main_quit)
    win.show_all()
    Gtk.main()
    
    # def authenticate():
    # 	twitter = Twitter(auth=OAuth('', '', CONSUMER_KEY, CONSUMER_SECRET), format='', api_version=None)
    # 	oauth_token =
    
    # CONSUMER_KEY = "3VXjHiLw4SmGQA1wubvOD8jyX"
    # CONSUMER_SECRET = "YrcdjaAWpM9w6i0rcW84HrLoSjoCH6Rz2Zam9DNFQ9Le3JSIx5"
    # TWITTER_CREDS = os.path.expanduser('~/twitter-creds')
    # if not os.path.exists(TWITTER_CREDS):
    # 	oauth_dance("Bird", CONSUMER_KEY, CONSUMER_SECRET, TWITTER_CREDS)
    #
    # oauth_token, oauth_secret = read_token_file(TWITTER_CREDS)
    #
    # t = Twitter(auth=OAuth(oauth_token, oauth_secret, CONSUMER_KEY, CONSUMER_SECRET))
    #
    # print(str(t.statuses.home_timeline()))
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

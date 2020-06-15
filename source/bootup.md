---
title: bootup
date: 2020-05-07
---
Example Python program bootup.py
For Python version 2.x.
To test your Python version use:

    python --version

## Modules

* import time
* from time import sleep
* from pygame import mixer
* import easygui
* import sys
* import Tkinter

## Methods

* def stopwatch():
* def alarm():
* def alarm_clock():

## Code

Python tkinter example

    '''
    This is the current side project I'm working on. It is primarily a terminal based alarmclock/stopwatch.
    Users get to pick between an Alarmclock and a stopwatch.
    I've added GUI support from simplegui library for now. However, this is very minimal.
    '''
    
    #TODO
    '''
    Adding radiobuttons with timezones
    Default timezone from the system time
    Adding a better gui with Tkinter
    '''
    
    import time
    from time import sleep
    from pygame import mixer
    import easygui
    import sys
    import Tkinter
    
    root = Tkinter.Tk()
    root.title("Alarm/Stopwatch")
    root.minsize(width=200, height=100)
    
    def stopwatch():
    	minutes = int(input("Countdown from:"))
    	ticker = minutes * 60
    	while ticker > 0:
    		label['text'] = str(ticker)
    		time.sleep(1)
    		root.update()
    		print str(ticker)
    		ticker -= 1
    	print("TIME'S UP!!!!")
    
    def alarm():
    	print "WAAAKE UP!!!!"
    	mixer.init()
    	mixer.music.load('/home/divya/Music/pink')
    	mixer.music.play()
    	# easygui.msgbox(msg="Time up!!!!", title= "J.A.R.V.I.S")
    
    def alarm_clock():
    	hours = float(easygui.enterbox(msg='Please enter the hours: 0-23', title='Hours', default=''))
    	if hours < 0 or hours > 23:
    		print "Invalid value for hours, should be >= 0 or <=23"
    		sys.exit(1)	
    	# print print_out
    	# hours = float(input("Please enter the hours? 0 to 23 "))
    	minutes = float(easygui.enterbox(msg='Please enter the minutes: 0-59', title='Minutes', default=''))
    
    	# minutes = float(input("Please enter the minutes?  "))
    
    	if minutes < 0 or minutes > 59:
    		print "Invalid value for minutes, should be >= 0 or <=59"
    		sys.exit(1)
    
    	now_hour = time.strftime("%H")
    	now_min = time.strftime("%M")
    	now_sec = time.strftime("%S")
    
    	if float(now_hour) != hours or float(now_min) != minutes:
    		min_hours = (hours - float(now_hour))
    		min_mins = minutes - float(now_min)
    		total = (min_hours*60) + min_mins
    		sec = (total * 60) - float(now_sec)
    
    		if min_mins == 1:
    			unit_word = "minute"
    		else:
    			unit_word = "minutes"
    
    		if total > 0:
    			if total < 60:
    				print "Sleeping for", int(total), unit_word
    			else:
    				print "Sleeping for", int(min_hours), "hours and", int(min_mins), unit_word
    			sleep(sec)
    			alarm()
    			msg = "Click \"Continue\" to snooze for 10 minutes"
    			title = "J.A.R.V.I.S"
    			if easygui.ccbox(msg, title):
    				print "Snoozing for 10 minutes"
    				mixer.music.stop()
    				sleep(600)
    				alarm()
    		else:
    			for i in range(5):
    				print "Alarm ringing!!", chr(7)
    				sleep(1)
    				
    label = Tkinter.Label(root, text='Watch this space for stopwatch')
    label.grid(row=2, column=5, columnspan=2)
    
    msg     = "Pick an option"
    title   = "Alarm/Stopwatch"
    choices = ["Alarmclock", "Stopwatch"]
    choice   = easygui.choicebox(msg, title, choices)
    if choice == "Alarmclock":
    	alarm_clock()
    elif choice == "Stopwatch":
    	stopwatch()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

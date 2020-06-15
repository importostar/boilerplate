---
title: angle_clock_hands
date: 2020-05-07
---
Example Python program angle_clock_hands.py
Python version 3.x or newer.
To check the Python version use:

    python --version


## Methods

* def solution(hour, minutes):

## Code

Python example

    # Given a time, calculate the angle between the hour and minute hands on a clock.
    
    hour = 3
    minutes = 27
    
    def solution(hour, minutes):
    	minute_percentage = float(minutes) / 60
    	minute_degrees = minute_percentage * 360
    	hour_degrees = float(hour)/12 * 360
    	next_hour = (hour + 1) % 12
    	if hour == 11:
    		next_hour_degrees = 360
    	else:
    		next_hour_degrees = float(next_hour)/12 * 360
    	in_between = minute_percentage * (next_hour_degrees - hour_degrees)
    	answer = minute_degrees - (hour_degrees + in_between)
    	return answer
    
    print(solution(3,27))
    print(solution(9,40))
    print(solution(11,10))
    print(solution(11,50))
    
    # The "official solution" formula is 30 * hours - 5.5 * minutes.

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

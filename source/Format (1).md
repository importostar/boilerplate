---
title: Format (1)
date: 2020-05-07
---
Example Python program Format (1).py
Python version 3.x or newer.
To check the Python version use:

    python --version


## Methods

* def stars(format, inp):
* def commas(inp):
* def dec(format, inp):
* def dollar(inp):
* def sDollar(inp):
* def exp(format, inp):

## Code

Python example

    def stars(format, inp):
    	starct = 0
    	for c in format:
    		if c == '&':
    			starct += 1
    	numct = 0
    	for c in inp:
    		if not c == '.':
    			numct += 1
    	if starct < numct:
    		print("more digits than stars")
    	return '*' * (starct-numct) + inp
    def commas(inp):
    	#for i in range(inp.find('.')-3,0, -3): #insert comma before each of these chars at these indices
    	for i in range(len(inp)-3,0, -3):
    		inp = inp[0:i] + ',' + inp[i:]
    	return inp
    
    def dec(format, inp):
    	decplace = len(format[format.find('.')+1:])
    	print(decplace)
    	decLoc = inp.find('.')
    	if not decLoc == -1:
    		currPlaces = len(inp[decLoc + 1:])
    	else:
    		decLoc = len(inp)
    		inp = inp + '.'
    		currPlaces = 0
    	print(currPlaces)
    	if(currPlaces <= decplace):
    		inp = inp + '0' * (decplace-currPlaces)
    	else:
    		#print(inp)
    		if((int(inp[decLoc + decplace + 1])) >= 5):
    			inp = inp[:decLoc + decplace] + (str(int(inp[decLoc + decplace]) + 1))
    		else:
    			inp = inp[:decLoc + decplace+1]
    	return (inp)
    def dollar(inp):
    	lastStarI = inp.rfind('*')
    	return '$' + inp[lastStarI + 1:]
    def sDollar(inp):
    	lastStarI = inp.rfind('*')
    	return inp[:lastStarI + 1] + '$' + inp[lastStarI +1:]
    def exp(format, inp):
    	oldlen = len(inp)
    	if not inp.find('.') == -1:
    		oldlen = len(inp[:inp.find('.')])
    		inp = inp[:inp.find('.')] + inp[inp.find('.') + 1:]
    	space = 0
    	for c in format:
    		if c == '&':
    			space += 1 
    	print(space)
    	if space < len(inp) and int(inp[space]) >= 5: #then round
    		inp = inp[:space - 1] + str(int(inp[space-1])+1)
    	elif space < len(inp) and int(inp[space]) < 5:
    		inp = inp[:space]
    	elif space > len(inp):
    		inp = inp + '0' * (space-len(inp))
    	inp = inp[:1] + '.' + inp[1:] + 'E' + str(oldlen - 1)
    	return inp
    	
    st = "&&&&E, 124353"
    format, inp = st.rstrip().split(", ")[0], st.rstrip().split(", ")[1]
    print(format)
    if(format[-1]=='E'):
    	inp = exp(format, inp)
    #print(inp)
    else:
    	if not format.find('.') == -1:
    		inp = dec(format, inp)
    	#print(inp)
    	inp = stars(format,inp)
    	#print(inp)
    	if not format.find(',') == -1:
    		inp = commas(inp)
    	#print(inp)
    	if format[0] == '$':
    		inp = dollar(inp)
    	#print(inp)
    	if format[0] == '*':
    		inp = sDollar(inp)
    	#print(inp)
    print(inp)

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

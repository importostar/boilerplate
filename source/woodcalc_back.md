---
title: woodcalc_back
date: 2020-05-07
---
Example Python program woodcalc_back.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import Tkinter as tkinter

## Methods

* def amount_wood(length, width, height):
* def times_beds(num_beds):
* def amt_sides(height):
* def board_size(sides, length, width):
* def result_print(board_size, amt_sides):

## Code

Python tkinter example

    """!!!!!!Infinite loop!!!!!
    Calculator takes input from user and calculates materials for building garden beds
    of a particular demension. User inputs demensions, width length and height
    of garden bed in feet, as well as the number of beds to be built. All
    outputs are in feet. Outputs include the total number feet needed of 2 by
    six lumber to build the beds, and calculates the most effecient use of the
    lumber by iterating through a list of standard board lengths."""
    
    import Tkinter as tkinter
    
    # calculates total amount of wood per bed
    def amount_wood(length, width, height):
    	total = 0
    	length = length * 2
    	width = width * 2
    	feet = length + width
    	if height == 6 or height == .5:
    		total = feet
    	elif height == 1:
    		total = feet * 2
    	elif height == 1.5:
    		total = feet * 3
    	elif height == 2:
    		total = feet * 4
    	elif height > 2:
    		return 'no calculation for height over two'
    	else:
    		return 'need specific height in'
    	return total
    
    #calculate amount of wood for all beds
    def times_beds(num_beds):
    	return feet * num_beds
    
    # determine total amount of side peices needed. Same for long and short
    def amt_sides(height):
    	sides = 0
     	if height == 6 or height == .5:
    		height = 1 
    	elif height == 1:
    		height = 2 
    	elif height == 1.5:
    		height = 3 
    	elif height == 2:
    		height =  4
    	else:
    		return 'need specific height in'
    	sides += height * 2 * num_beds
    	return sides 
    
    
    # determine most effecient use of materials with least amount of cuts
    def board_size(sides, length, width):
            boardlist = [8, 12, 16, 20, 24]
    	new_boardlist = []
    	long_sides = sides
    	wide_sides = sides
            while long_sides > 0:
                    for size in boardlist:
    			if size >= length and size % length  >= 0:
    				new_boardlist.append(size)
    				long_sides -= 1
    				break
    	while wide_sides > 0:	
    		for size in boardlist:
    			if size >= width and size % width >= 0:
    				new_boardlist.append(size)
    				wide_sides -= 1
    				break
            					
    	return (str(new_boardlist.count(8)) + " eight foot" +', '+ str(new_boardlist.count(12))
    + " twelve foot" + ', '+ str(new_boardlist.count(16)) + " sixteen foot" +' ,'+ str(new_boardlist.count(20))
    + " twenty foot" +' ,'+ str(new_boardlist.count(24)) + " twenty-four foot")
    
    # Combine two output functions for GUI label	
    def result_print(board_size, amt_sides):
        global width
        global length
        global height
        global num_beds
        sides = amt_sides(height)
        board_size(sides, length, width)
    
    ## Make a Tkinter GUI
    #create a window
    window = tkinter.Tk()
    
    #name the window
    window.title('woodcalc')
    
    #set window size
    #window.geometry('300x300')
    
    #create column of lables for text fields
    lbllen = tkinter.Label(window, text = "Length")
    lbllen.grid(row = 0, column = 0)
    lblwid = tkinter.Label(window, text = "Width")
    lblwid.grid(row = 1, column = 0)
    lblht = tkinter.Label(window, text = "Height")
    lblht.grid(row = 2, column = 0)
    lblamt = tkinter.Label(window, text = "Amt of Beds")
    lblamt.grid(row = 3, column = 0)
    
    # create text fields to match the labels
    entlen = tkinter.Entry(window)
    entlen.grid(row = 0, column = 1)
    entwid = tkinter.Entry(window)
    entwid.grid(row = 1, column = 1)
    entht = tkinter.Entry(window)
    entht.grid(row = 2, column = 1)
    entamt = tkinter.Entry(window)
    entamt.grid(row = 3, column = 1)
    
    #Store Variables needed for function args
    width = entwid.get()
    
    length = entlen.get()
    
    height = entht.get()
    
    num_beds = entamt.get()
    
    feet = amount_wood(length, width, height)    
    
    sides = amt_sides(height)
    
    
    #create a calculate button to run the functions
    calcbtn = tkinter.Button(window, text = "CALCULATE", command = result_print(board_size, amt_sides))
    calcbtn.grid(row = 5, columnspan = 2)
    
    #Label that prints output
    result = tkinter.Label(window, text = "Results")
    result.grid(row = 6, columnspan = 2)
    
    window.mainloop()
    
    ## Old code from before GUI, keeping for reference
    #width = float(raw_input('enter width '))
    
    #length = float(raw_input('enter length '))
    
    #height = float(raw_input('enter height '))
    
    #feet = amount_wood(length, width, height)
    
    #num_beds = float(raw_input('how many beds of size?'))
    
    #sides = amt_sides(height)
    
    #print feet
    
    #print times_beds(num_beds)
    
    #print ('you need ' + str(sides) +', '+ str(length) +
    # ' foot boards, and ' + str(sides) +', '+ str(width)
    #+ ' foot boards.')
    
    #print board_size(sides, length, width,)
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

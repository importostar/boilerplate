---
title: coursebook
date: 2020-05-07
---
Example Python program coursebook.py

## Modules

* from tkinter import *
* from tkinter import messagebox
* import tkinter.messagebox

## Classes

* class CourseApp():
* #	addClass:	Adds a class to the class ListBox. 
* #	remClass:	Removes a class from the class Listbox.

## Methods

* 	def __init__(self, parent):
* 	def addProf(self):
* 	def remProf(self):
* 	def addClass(self):
* 	def remClass(self):
* 	def addEntry(self):
* 	def remEntry(self):
* 	def remEntryAct(self):
* 	def syncEntries(self):
* 	def quit(self):

## Code

Python tkinter example

    #!/usr/bin/python3
    # CMPS 499 python assignment designed to work on python 3.2.3
    #
    # Problem Statement: Write a python script that manages faculty course assignments.
    #					 The solution should map faculty names to a list of courses they teach.
    #
    # Requirements:		 Add/Remove professors and classes
    #					 Assign a single Professor to a class
    #					 Remove an assignment
    #					 Display assignments
    #					 Must be graphical, interactive, menu-driven using Tcl/Tk in Python
    #
    # Last Modified - 04/24/2014: Minor changes for code readability.
    #
    # USER GUIDE: Python 3.2.3 is required along with Tkinter properly
    #			  installed for the app to function.
    #		
    #			  On startup, there will be 2 entry fields. Classes are
    #			  to be put in a CCCCXXX-SSS format, where C denotes the
    #			  class abbreviation, X is the course number, and S is the
    #			  section number. Professors are to be put in by surname
    #			  and last name I.E: Dr.Radle.
    #
    #			  One can add and remove professors and classes to the
    #			  lists by their respective buttons. To add in an
    #			  assignment, select a professor and class in the lists
    #			  and click on Add Assignment. Removing an assignment
    #			  brings up a separate window from where one can
    #			  select a assignment to remove.
    #
    # TODO: Use cpickle to keep persistent course management data using
    #		file I/O.
    # Licensed under BSD
    
    # Import tkinter
    
    from tkinter import *
    from tkinter import messagebox
    import tkinter.messagebox
    
    # Create the class to handle the CourseBook application object.
    
    class CourseApp():
    	
    # Initializes the CourseApp object.
    	
    	def __init__(self, parent):
    	
    #		Create a dictionary for courselist, and lists for classes
    #		professors.
    		
    		self.courselist = {}
    		self.classes = []
    		self.profs = []
    
    #		Initialize the frame that holds the entry widgets.
    		
    		entryFrame = Frame(parent)
    		entryFrame.pack()
    		entLabel = Label(entryFrame, text = "Professor & Course Entry")
    		entLabel.pack()
    		entLabel.grid(row=1, column=1)
    		self.profField = Entry(entryFrame, text = "Professor", width=30)
    		self.profField.insert(0, "Dr. Radle")
    		self.profField.pack()
    		self.profField.grid(row=2, column=1)
    		self.courseField = Entry(entryFrame, text = "course", width=30)
    		self.courseField.insert(0, "CMPS499-001")
    		self.courseField.pack()
    		self.courseField.grid(row=3, column=1)
    		
    #		Initialize the frame that holds the buttons.
    
    		buttonFrame = Frame(parent)
    		buttonFrame.pack()
    
    #		Create and add the buttons.
    
    		paddButton = Button(buttonFrame, text="Add Professor", width = 30, command = self.addProf)
    		paddButton.pack(side = BOTTOM)
    		caddButton = Button(buttonFrame, text="Add Class", width = 30, command = self.addClass)
    		caddButton.pack(side = BOTTOM)
    
    		premButton = Button(buttonFrame, text="Remove Professor", width = 30, command = self.remProf)
    		premButton.pack(side = BOTTOM)
    		cremButton = Button(buttonFrame, text="Remove Class", width = 30, command = self.remClass)
    		cremButton.pack(side = BOTTOM)
    
    
    		pclaButton = Button(buttonFrame, text="Add Assignment", width = 30, command = self.addEntry)
    		pclaButton.pack(side = BOTTOM)
    		pclrButton = Button(buttonFrame, text="Remove Assignment", width = 30, command = self.remEntry)
    		pclrButton.pack(side = BOTTOM)
    
    #		Initialize the frame that holds the listboxes and create the list.		
    
    		listFrame = Frame(parent)
    		listFrame.pack()
    
    		clabel = Label(listFrame, text = "Classes                       Professors")
    		clabel.pack(side= TOP)
    
    		self.classListBox = Listbox(listFrame)	
    		self.classListBox.pack( side = LEFT )
    
    		self.profListBox = Listbox(listFrame)
    		self.profListBox.pack( side = LEFT )
    
    		listFrame2 = Frame(parent)
    		listFrame2.pack()
    		clabel2 = Label(listFrame2, text = "Assignments")
    		clabel2.pack(  )
    		
    		self.clabel3 = Label(listFrame2, text = "")
    		self.clabel3.pack(  )
    
    #		Originally used a ListBox widget implementation for the assignments.
    #		Found generating labels from the dictionary easier to work with.
    #		self.pclListBox = Listbox(listFrame2, width = 40)
    #		for prof,course in courselist :
    #			pclListBox.insert(END, prof, course)
    #		self.pclListBox.pack( side = BOTTOM )
    
    #	Coursebook Functions:
    #	-----------------------------------------------------------------------
    #	addProf:	Adds a professor from the Professor Entry Widget to the 
    #			professor ListBox.
    #	-----------------------------------------------------------------------
    
    	def addProf(self):
    		profadd = self.profField.get()
    		self.profListBox.insert(END, (profadd))
    		self.syncEntries
    
    #	-----------------------------------------------------------------------
    #	remProf:	Removes selected professor in the professor ListBox.
    #			TODO: Remove all classes professor is teaching from
    #			the courselist dictionary.
    #	-----------------------------------------------------------------------
    
    	def remProf(self):
    		profname = self.profListBox.get(ACTIVE)
    		self.profListBox.delete(ANCHOR)
    		self.syncEntries
    
    #	-----------------------------------------------------------------------
    #	addClass:	Adds a class to the class ListBox. 
    #	-----------------------------------------------------------------------
    
    	def addClass(self):
    		classadd = self.courseField.get()
    		self.classListBox.insert(END, (classadd))
    		self.syncEntries
    
    #	-----------------------------------------------------------------------
    #	remClass:	Removes a class from the class Listbox.
    #				TODO: Remove all classes that are in assignments.
    #	-----------------------------------------------------------------------
    
    	def remClass(self):
    		classname = self.classListBox.get(ACTIVE)
    		self.remEntry
    		self.classListBox.delete(ANCHOR)
    		self.syncEntries
    
    #	-----------------------------------------------------------------------
    #	addEntry:	Adds a label to the assignment Listbox with the name of
    #				the professor and the class they are teaching.
    #				Gets professor and class from the active selection in their
    #				respective listboxes.
    #	-----------------------------------------------------------------------
    
    	def addEntry(self):
    		profname = self.profListBox.get(ACTIVE)
    		classadd = self.classListBox.get(ACTIVE)
    		self.courselist[classadd] = profname
    		self.clabel3['text'] = '\n'.join('{} {}'.format(k, d) for k, d in self.courselist.items())
    		self.clabel3.pack()
    		self.syncEntries	
    
    #	-----------------------------------------------------------------------
    #	remEntry:	Brings up a window that prompts for a selection in
    #				the assignments. Creates a button that will take the
    #				selection and invoke remEntryAct.
    #	-----------------------------------------------------------------------
    
    	def remEntry(self):
    
    #		Initialize new window, create frame to hold Listbox.
    
    		clwin = Toplevel()
    		clwin.wm_title("Remove Assignment Entry")
    		remFrame = Frame(clwin)
    		remFrame.pack()
    
    		cllab = Label(clwin, text="Select the class to remove it as an assignment.")
    		cllab.pack()
    
    		self.remListBox = Listbox(remFrame)
    		testclass = self.classListBox.get(0,END)
    		
    #		Populate the listbox.
    
    		for courses in testclass:
    			self.remListBox.insert(END, courses)
    		self.remListBox.pack( side = BOTTOM )
    		
    #		Create button that will invoke the actual act of removing an entry.		
    		
    		remButton = Button(remFrame, text="Remove Assignment", width = 30, command = self.remEntryAct)
    		remButton.pack(side = BOTTOM)
    
    #	-----------------------------------------------------------------------
    #	remEntryAct:	Removes the course from the courselist dict by the
    #					course key.
    #	-----------------------------------------------------------------------
    	
    	def remEntryAct(self):
    		courserem = self.remListBox.get(ACTIVE)
    		self.courselist.pop(courserem, None)
    		self.remListBox.delete(ANCHOR)
    		self.clabel3['text'] = '\n'.join('{} {}'.format(k, d) for k, d in self.courselist.items())
    		self.clabel3.pack()
    		self.syncEntries		
    
    #	-----------------------------------------------------------------------
    #	remProf:	Removes selected professor in the professor ListBox.
    #			TODO: Remove all classes professor is teaching from
    #			the courselist dictionary.
    #	-----------------------------------------------------------------------
    
    	def syncEntries(self):
    		self.profs = self.profListBox.get(0,END)
    		self.classes = self.classListBox.get(0,END)
    
    ## TODO: Define a sync method that will update from the actual dict and lists to stay consistent.
    #  TODO: Add in an exit button that will call quit.	
    	def quit(self):
    		sys.exit()
    
    ## Initialize tkinter GUI window and run the application.
    
    root = Tk()
    root.title('Course Book')
    
    top = CourseApp(root)
    root.mainloop()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

---
title: To do list
date: 2020-05-07
---
Example Python program To-do-list.py

## Modules

* import Tkinter
* import tkMessageBox

## Methods

* def update_listbox():
* def clear_listbox(): # To clear the previous list otherwise items keeps repeating
* def add_task():
* def del_all():
* def del_one():
* def sort_asc():
* def sort_desc():
* def show_number_of_tasks():

## Code

Python tkinter example

    #!/usr/bin/python2.7
    
    # Simple To-Do-List GUI in python 2.7
    # Dhiraj Saharia
    import Tkinter
    import tkMessageBox
    
    root = Tkinter.Tk()
    
    #Change root window BG color
    root.configure(bg="white")
    
    #Change the title
    root.title("My To-Do-List")
    
    #Change the window size
    root.geometry("325x275")
    
    #Create empty list
    tasks = []
    #For testing using a default list
    tasks = ["Call Mom", "Buy Bread", "Buy Milk"]
    
    
    
    
    # Create Functions
    def update_listbox():
    	# Clear the current list
    	clear_listbox()
    	#Populate the listbox with tasks
    	for task in tasks:
    		lb_tasks.insert("end", task)
    
    def clear_listbox(): # To clear the previous list otherwise items keeps repeating
    	lb_tasks.delete(0, "end")
    
    def add_task():
    	# Get the task to add
    	task = txt_input.get()
    	if task != "":
    		# Append to list
    		tasks.append(task)
    		update_listbox()
    	else:
    		tkMessageBox.showwarning("WARNING", "You need to enter a task")
    	txt_input.delete(0, "end")
    
    def del_all():
    	confirmed = tkMessageBox.askyesno("Please Confirm", "Do you really want to delete all tasks?")
    	if confirmed == True:
    		# Since we are changing the list, it need to be global
    		global tasks 
    		#Clear the task list
    		tasks=[]
    		# Update listbox
    		update_listbox()
    
    def del_one():
    	# Get the text of selected task
    	task = lb_tasks.get("active")
    	# Confirm in the list
    	if task in tasks:
    		tasks.remove(task)
    	# Update the listbox
    	update_listbox()
    
    def sort_asc():
    	tasks.sort()
    	# Update the listbox
    	update_listbox()
    
    def sort_desc():
    	tasks.sort()
    	tasks.reverse() #Reverse the list for DESC
    	update_listbox()
    
    def show_number_of_tasks():
    	# Get the number of tasks
    	number_of_tasks = len(tasks)
    	msg = "Number of Tasks: %s" %number_of_tasks
    	# Display the msg in display window
    	lbl_display["text"] = msg
    
    
    
    
    
    lbl_title = Tkinter.Label(root, text="To-Do-List", bg="white") #Create Widget
    lbl_title.grid(row=0,column=0) #To have the buttons in a grid
    
    lbl_display = Tkinter.Label(root, text="", bg="white") # To add space after title
    lbl_display.grid(row=0,column=1)
    
    txt_input = Tkinter.Entry(root, width=15) #To entry Task
    txt_input.grid(row=1,column=1)
    
    # Buttons
    btn_add_task = Tkinter.Button(root, text="Add Task", fg="red", bg="white", command=add_task)
    btn_add_task.grid(row=1,column=0)
    
    btn_del_all = Tkinter.Button(root, text="Delete All Task", fg="red", bg="white", command=del_all)
    btn_del_all.grid(row=2,column=0)
    
    btn_del_one = Tkinter.Button(root, text="Delete One Task", fg="red", bg="white", command=del_one)
    btn_del_one.grid(row=3,column=0)
    
    btn_sort_asc = Tkinter.Button(root, text="Sort Task Ascending", fg="green", bg="white", command=sort_asc)
    btn_sort_asc.grid(row=4,column=0)
    
    btn_sort_desc = Tkinter.Button(root, text="Sort Task Desending", fg="green", bg="white", command=sort_desc)
    btn_sort_desc.grid(row=5,column=0)
    
    btn_number_of_tasks = Tkinter.Button(root, text="Number of Tasks", fg="red", bg="white", command=show_number_of_tasks)
    btn_number_of_tasks.grid(row=6,column=0)
    
    btn_exit = Tkinter.Button(root, text="Quit", fg="black", bg="white", command=exit) #Exit command is inbuilt
    btn_exit.grid(row=7,column=0)
    
    lb_tasks = Tkinter.Listbox(root)
    lb_tasks.grid(row=2,column=1,rowspan=6)
    
    
    root.mainloop()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

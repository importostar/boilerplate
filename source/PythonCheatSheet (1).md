---
title: PythonCheatSheet (1)
date: 2020-05-07
---
Example Python program PythonCheatSheet (1).py

## Modules

* import sys
* import json 
* import os
* import subprocess
* import Tkinter

## Classes

* class Object(InheritedObject):
* class Application(Frame):

## Methods

* 	def function(arguments):
* 	def __init__(self, master=None):
* 	def __init__(self, master=None):

## Code

Python tkinter example

    # I use python so infequently that i forget most of the stuff i learnt when next I need to use it.
    # Here are some frequently used commands. Python 3.5 NOT 2.7
    
    # System variables:
    
    __file__
    # Absolute path to current script
    
    # Basic Syntax:
    
    class Object(InheritedObject):
    # define class that inhereits from another class
    	def function(arguments):
    		pass
    	# member function
    	def __init__(self, master=None):
    	# constructor
            InheritedObject.__init__(self, master)
    		# call constructor from inhereited class
    		self.variable = 0
    		# member variables
    		
    if __name__ == "__main__":
    # if you want to use python file like a library this won't be called.
    	obj = Object()
    	obj.function()
    	
    ### SYS ###
    import sys
    
    for arg in sys.argv:
    	# ignore file argument
    	if arg == __file__: 
    		continue
    	if arg == "argument":
    		pass
    # Handling command line arguments
    sys.exit("""optional return int""")
    # exit script. 
    
    ### FILE IO ###
    
    # open a file with permissions. "r" = reading, "w" writing, "r+" reading and writing, "a" appending, "b" binary mode, "t" text mode
    with open('workfile', "rwb") as f:
    # above automatically closes file, otherwise close manually
    f = open('workfile')
    f.close()
    # read file to string in text mode, or bytes in binary mode
    f.read()
    # seek file position
    f.seek(0)
    
    ### JSON ###
    import json 
    
    with open("file.json", "r") as json_file:
        json_str = json_file.read()
    
    json_obj = json.loads(json_str)
    # do stuff here. json_obj is a regular dictionary object. 
    with open("map_model.json", "w") as json_file:
    	# use dumps format dict to file back to a json formatted str. 
        json_file.write(json.dumps(json_obj))  
    
    ### ARGPARSE ###
    
    parser = argparse.ArgumentParser(formatter_class=argparse.RawDescriptionHelpFormatter,
                                     description=textwrap.dedent('''Discription'''),
                                     epilog='''Written by Peter Respondek''')
    parser.add_argument("-r", help="directories will be relative to this position")
    # optional argument
    parser.add_argument("root", help="start directory")
    # positional argument
    argv = parser.parse_args()
    var = argv.r
    # get -r argument
    
    ### OS ###
    import os
    
    os.chdir
    # Change the current working directory to path.
    os.utime("path", None)
    # touch time modified tim
    os.remove("path/to/file")
    # delete file
    path = os.getcwd()
    # current working directory
    
    ### OS.PATH ###
    
    os.path.isfile("path/to/file")
    # check if file exists
    os.path.exists("path/to/file")
    # check if path exists
    name,ext = os.path.splitext("filename")
    # Split filename and extension
    path,file = os.path.split("path")
    # Split filename and file dir
    time = os.path.getmtime("filename")
    # Get file modified time
    path = os.path.relpath("/path/to/file1", "/path/to/file1")
    # Relatve path between two directories
    path = os.path.expanduser("~/path/to/file")
    # Get absolute path to file which has user shortcut
    path = os.path.join("path","filename")
    # join two paths
    for (dirpath, dirnames, filenames) in os.walk("path"):
    # recursively iterate through path 
    
    
    ### SUBPROCESS ###
    import subprocess
    
    returncode = subprocess.call(['command', 'args'])
    # make system call and wait for it to finish.
    subprocess.check_call(['command', 'args'])
    # make system call and wait for it to finish. raise CalledProcessError if it doesn't work.
    
    ### RE ###
    
    ### TKINTER ###
    import Tkinter
    
    # use file extenstion .pyw for scripts using tkinter to automatically open GUI
    
    class Application(Frame):
    	def __init__(self, master=None):
    		Frame.__init__(self, master)
    		self.grid(sticky=N+S+E+W)
    		Grid.rowconfigure(self, 0, weight=1, minsize=70)
            	Grid.rowconfigure(self, 1, weight=1, minsize=70)
    		Grid.columnconfigure(self, 0, weight=1)
            	Grid.columnconfigure(self, 1, weight=1)
    		
    		frame = LabelFrame(self, text="Frame Name")
            	Grid.columnconfigure(frame, 0, weight=1)
    		Grid.rowconfigure(frame, 0, weight=1)
    		frame.grid(row=0, padx=5, columnspan = 2, pady=5, sticky=N+S+E+W)
    		
    		scrollbar = Scrollbar(frame)
            	scrollbar.grid(row=0,column=1,padx=(0,5),pady=5, sticky=N+S+E+W)
            	self.console.config(yscrollcommand=scrollbar.set)
            	scrollbar.config(command=self.console.yview)
    		
    		button = Button(frame, text = "Button", command = buttonFunction)
    		button.config(state="active", relief=RAISED)
            	button.grid(row=1,column=0,padx=5,pady=5, sticky=N+S+E+W)
    		
    		listbox = Listbox(frame)
    		listbox.bind("<Up>", self.function)
    		#bind input to function
    		
    		textbox = Text(frame, wrap=NONE)
            	textbox.tag_config("intro", foreground="blue")
            	textbox.insert(END,"TEXT!")
    
    root = Tk()
    root.title("App Name")
    root.minsize(600,600)
    Grid.rowconfigure(root, 0, weight=1)
    Grid.columnconfigure(root, 0, weight=1)
    app = Application(master=root)
    root.protocol("WM_DELETE_WINDOW", app.shutdown)
    app.mainloop()
    # basic setup

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

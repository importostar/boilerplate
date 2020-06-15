---
title: comparatore
date: 2020-05-07
---
Example Python program comparatore.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import csv
* import tkinter
* from tkinter.filedialog import askopenfilename

## Methods

* def close_window(): # destroying the main window
* def file_A(): # return file rif
* def file_B():
* def diff(a, b):
* def esegui():

## Code

Python tkinter example

    #!/usr/bin/python3
    import csv
    import tkinter
    from tkinter.filedialog import askopenfilename
    
    A = ''
    B = ''
    
    def close_window(): # destroying the main window
        root.destroy() 
    		
    def file_A(): # return file rif
    	globals()['A'] = askopenfilename()
    
    def file_B():
    	globals()['B'] = askopenfilename()
    
    def diff(a, b):
        b = set(b)
        return [aa for aa in a if aa not in b]
    
    def esegui():
    	file1 = open(A, "r")
    	file2 = open(B, "r")
    
    	reader1 = csv.reader(file1, delimiter=';', quotechar=' ')
    	reader2 = csv.reader(file2, delimiter=';', quotechar=' ')
    
    	lista1 = []
    	lista2 = []
    
    	for row in reader1:
    	    lista1.append(str(row[0]))
    	for row in reader2:
    	    lista2.append(str(row[0]))
    
    	f = open("diff.txt","w+")
    	f.write("Telai che differiscono tra spunta e nave\n")
    	
    	out = diff(lista2, lista1) or diff(lista1, lista2)
    	if len(out) == 0:
    		print('nothing to do')
    		exit()
    	else:
    		print('differenze')
    		for i in out:
    			print(i)
    			print(i, file=f)
    		f.close()
    
    root = tkinter.Tk()
    root.title("Comparatore di Telai")
    root.withdraw()
    root.update_idletasks()  # Update "requested size" from geometry manager
    
    x = (root.winfo_screenwidth() - root.winfo_reqwidth()) / 2
    y = (root.winfo_screenheight() - root.winfo_reqheight()) / 2
    root.geometry("+%d+%d" % (x, y))
    root.deiconify()
    
    frame = tkinter.Frame(root)
    frame.pack()
    
    button_open_A = tkinter.Button(frame)
    button_open_A['text'] = 'Seleziona la lista di sbarco'
    button_open_A['command'] = file_A
    button_open_A.pack()
    
    button_open_B = tkinter.Button(frame)
    button_open_B['text'] = 'Seleziona la spunta effettuata'
    button_open_B['command'] = file_B
    button_open_B.pack()
    
    button_run = tkinter.Button(frame)
    button_run['text'] = 'Compara le liste'
    button_run['command'] = esegui
    button_run.pack()
    
    button_kill = tkinter.Button(frame)
    button_kill['text'] ="Exit"
    button_kill['command'] = close_window
    button_kill.pack()
    
    tkinter.mainloop()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

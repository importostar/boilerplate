---
title: pomodoro
date: 2020-05-07
---
Example Python program pomodoro.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import time
* import datetime as dt
* import tkinter
* from tkinter import messagebox
* from tkinter import simpledialog
* from tkinter import Button
* import os

## Methods

* def play_sound():
* def quit():
* def check():

## Code

Python tkinter example

    #! /usr/bin/env python3
    
    import time
    import datetime as dt
    
    import tkinter
    from tkinter import messagebox
    from tkinter import simpledialog
    from tkinter import Button
    import os
    
    
    def play_sound():
    	file = "/home/santiago/Music/alert.wav"
    	os.system("play " + file)
    
    
    def quit():
    	global root
    	root.destroy()
    
    
    def check():
    	global t_now, t_fut, t_fin, total_pomodoros, timenow, root, answer
    	if t_now < t_fut:
    		print('First tnow < tfut')
    	# Commented out. Uncomment to add a break of 5 mins into the comodoro!
    	# it is now past working pomodoro, within the break. Delete the websites
    	elif t_fut <= t_now <= t_fin:
    		print('Break time!')
    	# Pomodoro and break finished. Check if ready for another pomodoro!
    	else:
    		print('Third tnow > tfut - Finished')
    		# Ring a bell (with print('\a') to alert of end of program.
    		print('\a')
    		# Annoy!
    		play_sound()
    		usr_ans = messagebox.askyesno(
    			"Termino el pomodoro!", "Queres empezar otro?")
    		total_pomodoros += 1
    		if usr_ans == True:
    			# user wants another pomodoro! Update values to indicate new timeset.
    			answer = simpledialog.askstring("Hola", "Que vas a hacer?",
    								parent=root)
    			t_now = dt.datetime.now()
    			t_fut = t_now + dt.timedelta(0, t_pom)
    			t_fin = t_now + dt.timedelta(0, t_pom+delta_sec)
    			root.after(1000, check)
    		elif usr_ans == False:
    			print("Terminamos! \nCompletaste " +
    				  str(total_pomodoros) + " pomodoros hoy.")
    			# unlock the websites
    			# Show a final message)
    			messagebox.showinfo("Pomodoro Finished!", "\nIt is now " + timenow +
    								"\nYou completed "+str(total_pomodoros)+" pomodoros today!")
    	t_now = dt.datetime.now()
    	timenow = t_now.strftime("%H:%M")
    	text = "Haciendo " + answer + " hasta las " + t_fin.strftime("%H:%M") + " siendo las " + timenow
    	labelTime.config(text=text, width="50")
    	root.after(20000, check)
    
    
    root = tkinter.Tk()
    root.geometry("400x400")
    Button(root, text="Salir", command=quit).pack()
    labelTime = tkinter.Label(root)
    labelTime.pack()
    
    total_pomodoros = 0
    
    
    t_now = dt.datetime.now()
    t_min = 25
    
    t_pom = t_min * 60
    
    t_delta = dt.timedelta(0, t_pom)
    
    t_fut = t_now + t_delta
    
    delta_sec = 1
    t_fin = t_now + dt.timedelta(0, t_pom+delta_sec)
    
    answer = simpledialog.askstring("Hola", "Que vas a hacer?",
    								parent=root)
    # GUI set pomodoro in motion!
    usr_ans = messagebox.askyesno("Arrancamos el Pomodoro!", "\nAhora son las "+t_now.strftime("%H:%M") +
    							  " hrs. \nLa alarma esta seteada a " + str(t_min) + " mins.")
    
    if usr_ans == True:
    	# root.iconify()
    	root.title("Trabajando")
    	text = "Haciendo " + answer + " hasta las " + t_fin.strftime("%H:%M")
    	labelTime.config(text=text, width="50")
    	t_now = dt.datetime.now()
    	timenow = t_now.strftime("%H:%M")
    	check()
    	root.mainloop()
    
    print('\n\nMade it to the end!\n\n')
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

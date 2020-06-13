---
title: cgpa_tkinter
date: 2020-05-07
---
Example Python program cgpa_tkinter.py

## Modules

* from tkinter import *
* from tkinter import messagebox
* 	if (gradess_this_sem<8.5): # very very important piece of code!!!!!!

## Methods

* def grade(grd):
* def calc_CG(event):

## Code

Python tkinter example

    from tkinter import *
    from tkinter import messagebox
    
    def grade(grd):
    	dictt = {'A':10,'A-':9,'B':8,'B-':7,'C':6,'C-':5,'D':4,'E':2}
    	return dictt[grd]
    
    def calc_CG(event):
    	print ("Calculating !")
    	gradess_this_sem = 0
    	creditss_this_sem = 0
    	for j in range (6):
    		gradess_this_sem = gradess_this_sem + int(creditss_list[j].get())*(grade(grades_list[j].get()))
    		creditss_this_sem = creditss_this_sem + int(creditss_list[j].get())
    	gradess_this_sem = gradess_this_sem/creditss_this_sem
    	if (gradess_this_sem<8.5): # very very important piece of code!!!!!!
    		emoji = "(︶︹︶)"
    	else:
    		emoji = "(̿▀̿‿ ̿▀̿ ̿)"
    	messagebox.showinfo(emoji, str(gradess_this_sem)+" CGPA")	
    
    top = tkinter.Tk()
    top.title("THE GREAT CGPA CALCUATOR")
    top.configure(background="black")
    
    CGPATEXT = Label(top, text = "The Great CGPA Calcuator", font=("Helvetica",20))
    CGPATEXT.pack()
    
    creditss_list = []
    grades_list = []
    
    L1 = Label(top, text = "¯\_(ツ)_/¯", bg="black", fg="white", font=("Helvetica",20))
    L1.pack()
    
    frame_2 = Frame()
    frame_2.pack()
    
    lbl_creditss = Label(frame_2,text="Credits :")
    lbl_creditss.grid(row=0,column=0)
    lbl_grades = Label(frame_2,text="Grades :")
    lbl_grades.grid(row = 0,column=1)
    
    for i in range (6):			
    			creditss_list.append(Spinbox(frame_2,values=(1,2,3,4,5,20)))
    			creditss_list[i].grid(row = i+1,column = 0,padx=10,pady=10)
    				
    			grades_list.append(Spinbox(frame_2,values = ("E","D","C-","B-","B","C-","A-","A")))
    			grades_list[i].grid(row = i+1,column=1,padx=10,pady=10)
    			
    btn_calcCG = Button(text="! Press with Caution !", bg="red", fg="white")
    btn_calcCG.bind("<Button-1>",calc_CG)
    btn_calcCG.pack(pady=8)
    
    top.mainloop()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

---
title: SquanchyGame
date: 2020-05-07
---
Example Python program SquanchyGame.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import tkinter as tk
* from tkinter import *
* #import functions
* import sqlite3 as sqlite
* from tkinter import font as tkFont
* from tkinter import ttk
* import sys, os
* from time import sleep
* import random
* from PIL import Image,ImageTk

## Classes

* # class Fun:
* class MainWindow(tk.Frame):

## Methods

* # def ran():
* def __init__(self, master=None):
* def random_pol_word(self):
* def random_eng_word(self):
* def check(self):
* # def chose_user():
* def window_popup(self):
* def adding_words1(self):

## Code

Python tkinter example

    import tkinter as tk
    from tkinter import *
    #import functions
    import sqlite3 as sqlite
    from tkinter import font as tkFont
    from tkinter import ttk
    import sys, os
    from time import sleep
    
    import random
    
    from PIL import Image,ImageTk
    
    
    conn = sqlite.connect('words.db')
    cur = conn.cursor()
    
    # class Fun:
    #
    #     def ran():
    #
    #         global los
    #         los=random.randint(1,1000)
    
    
    class MainWindow(tk.Frame):
        def __init__(self, master=None):
    
    
            tk.Frame.__init__(self, master)
    
            self.master = master
            
            self.master.geometry('725x350+500+200')
    
    
            menu=Menu(master)
            self.master.config(menu=menu)
    
            file = Menu(menu)
            file.add_command(label="jakas")
            file.add_command(label="New Game")
            file.add_command(label="New User")
            file.add_command(label="Change User")
    
            menu.add_cascade(label="File", menu=file)
    
            exit = Menu(menu)
            exit.add_command(label="Save and Exit")
            menu.add_cascade(label="Exit",menu=exit)
    
    
    
            self.pic_ang_to_pol = ImageTk.PhotoImage(Image.open("img/ang_to_pol.png"))
            self.pic_pol_to_ang = ImageTk.PhotoImage(Image.open("img/pol_to_ang.png"))
    
            self.random_button = Button(master, text="Get a Word",width=130,height=49,bd=0, command=self.random_eng_word)
            self.random_button.config(image=self.pic_ang_to_pol)
            self.random_button.place(x=195,y=30)
    
            self.random_button_2 = Button(master, text="Get a Word", width=130, height=49, bd=0,command=self.random_pol_word)
            self.random_button_2.config(image=self.pic_pol_to_ang)
            self.random_button_2.place(x=395,y=30)
    
    
            self.show_window = Label(master,width=24,justify=CENTER,highlightbackground="#ffa500",highlightthickness=3,font=("Lobster",16))
            self.show_window.config(highlightbackground="#ffa500")
            self.show_window.place(x=220,y=100)
    
            self.answer=Entry(master,width=24,justify=CENTER,bd=0,highlightbackground="#ffa500",highlightthickness=3,font=("Lobster",16))
            self.answer.config(highlightbackground="#ffa500")
            self.answer.place(x=220,y=155)
    
            self.check_button = Button(master, text="Check", width=4, height=1, bg="#ffa500", fg="#00247d", bd=0,activebackground="#ffa500",activeforeground="#00247d",font=("Lobster", 21), command=self.check)
            self.check_button.place(x=220, y=210)
    
    
            self.hint_img = ImageTk.PhotoImage(Image.open("img/hint.png"))
            self.hint_button=Button(height=55,width=55,bg="#ffa500",image=self.hint_img)
            self.hint_button.pack(anchor=NE)
    
            self.exit_img = ImageTk.PhotoImage(Image.open("img/exit.png"))
            self.exit_button = Button(height=55,width=55, bg="#2a3693",image=self.exit_img)
            self.exit_button.pack(anchor=NE)
    
            self.change_user_img = ImageTk.PhotoImage(Image.open("img/change_user.png"))
            self.hint3_button = Button(height=55, width=55,image=self.change_user_img)
            self.hint3_button.pack(anchor=NE)
    
            self.add_word_img = ImageTk.PhotoImage(Image.open("img/add_word.png"))
            self.hint3_button = Button(height=55, width=55, image=self.add_word_img)
            self.hint3_button.pack(anchor=NE)
    
            self.statistic_img = ImageTk.PhotoImage(Image.open("img/statistic.png"))
            self.hint3_button = Button(height=55, width=55, image=self.statistic_img)
            self.hint3_button.pack(anchor=NE)
    
    
            self.user = Label(master,text="Score: ",height=1,width=15,justify=LEFT, font=("Helvetica",10,"bold"))
            self.user.place(x=1,y=330)
    
        def random_pol_word(self):
    
            self.conn = sqlite.connect('words.db')
            self.cur = conn.cursor()
            self.cur.execute("""SELECT polish_word FROM table1 ORDER BY RANDOM() LIMIT 1;""")
            self.a = self.cur.fetchall()
            self.show_window.configure(text=str(self.a))
            print(self.a)
    
            self.conn.commit()
            self.conn.close()
    
    
        def random_eng_word(self):
    
            self.conn = sqlite.connect('words.db')
            self.cur = conn.cursor()
            self.cur.execute("""SELECT english_word FROM table1 ORDER BY RANDOM() LIMIT 1;""")
            self.a = self.cur.fetchall()
            self.show_window.configure(text=str(self.a))
            print(self.a)
    
            self.conn.commit()
            self.conn.close()
    
        def check(self):
            print("Dupa")
            self.random_obj=self.show_window.cget("text")
            self.answer_word_obj=self.answer.get()
    
    
            self.top2 = Toplevel()
            self.good_label = Label(Toplevel,text="Dobrze", height=2,width=10)
            self.good_label.place(x=230,y=210)
    
    
            # if self.random_obj == self.answer_word_obj:
            #
            #     self.good_label = Label(master=app,text="Dobrze",height=30,width=50)       ########### FUNKCJA NIE DZIAŁA. nAPRAWIC I USUNAC PRINTY
            #     #self.good_label.place(x=260,y=210)
            #     self.good_label.pack()
            #     sleep(3)
            #     self.good_label.destroy()
            #     print("Dupa2")
            #
            #
            # else:
            #     self.good_label = Label(master=app,text="Zle",height=30,width=50)
            #     self.good_label.place(x=260, y=210)
            #     sleep(3)
            #     self.good_label.destroy()
            #     print("Dupa3")
            #
            # def chose_user():
            #     pass
    
    
    
        def window_popup(self):
            self.top = Toplevel()
    
    
    
            self.label_1 = Label(self.top, text="Insert 1st English", font=("Helvetica", 11), bg="#7793d4")
            self.label_1.grid(row=0,column=0)
    
            self.entry_1 = Entry(self.top, bg="#7793d4", bd=2)
            self.entry_1.delete(0, END)
            self.entry_1.config(highlightbackground="red")
            self.entry_1.grid(row=1, column=0, pady=4)
            self.firstEn = self.entry_1.get()
            
            return self.top
    
    
    
        def adding_words1(self):
    
            en1_add_to_db = self.entry1.get()
            self.entry1.delete(0,END)
    
            en2_add_to_db = self.entry2.get()
            self.entry2.delete(0, END)
    
            en3_add_to_db = self.entry3.get()
            self.entry3.delete(0, END)
    
            en4_add_to_db = self.entry4.get()
            self.entry4.delete(0, END)
    
            pl1_add_to_db = self.entry5.get()
            self.entry5.delete(0, END)
    
            pl2_add_to_db = self.entry6.get()
            self.entry6.delete(0, END)
    
            pl3_add_to_db = self.entry7.get()
            self.entry7.delete(0, END)
    
            pl4_add_to_db = self.entry8.get()
            self.entry8.delete(0, END)
    
    
            list_of_fields=[en1_add_to_db, en2_add_to_db, en3_add_to_db, en4_add_to_db,
                            pl1_add_to_db, pl2_add_to_db, pl3_add_to_db, pl4_add_to_db]
    
    
    
            cur.execute("""INSERT INTO table1(english_word, english_word_1, english_word_2, english_word_3,
                        polish_word, polish_word_1, polish_word_2, polish_word_3) VALUES(?,?,?,?,?,?,?,?)""",list_of_fields)
            conn.commit()
    
    
    
    root = Tk()
    app = MainWindow(root)
    app.master.title("Squanchy Game")
    app.master.configure(background='#7793d4')
    app.mainloop()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

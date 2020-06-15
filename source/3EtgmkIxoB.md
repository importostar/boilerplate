---
title: 3EtgmkIxoB
date: 2020-05-07
---
Example Python program 3EtgmkIxoB.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import pymysql.cursors
* import pymysqlpool
* from tkinter import *
* from datetime import datetime
* import tkinter.ttk
* from PIL import *
* import os

## Classes

* class DBExecutor():

## Methods

* 	def __init__(self, **connection_params):
* 	def _connect(self):
* 	def execute(self, sql, *args, **kwargs):
* def create_widgets_in_first_frame():
* def quitApp():
* def quitApp2():
* def create_widgets_in_second_frame():
* def select_item(event):
* def select_item(event):
* def create_widgets_in_third_frame():
* def change(event=None):
* def call_first_frame_on_top():
* def call_second_frame_on_top():
* def call_third_frame_on_top():
* def quit_program():

## Code

Python tkinter example

    import pymysql.cursors
    import pymysqlpool
    from tkinter import *
    from datetime import datetime
    import tkinter.ttk
    from PIL import *
    import os
    
    
    
    class DBExecutor():
    	def __init__(self, **connection_params):
    		self._connection_params = connection_params
    		self._connection = None
    
    	def _connect(self):
    		self._connection = pymysql.connect(**self._connection_params)	
    	def execute(self, sql, *args, **kwargs):
    		if not (self._connection and self._connection.ping(True)):
    			self._connect()
    		with self._connection.cursor() as cursor:
    			cursor.execute(sql, *args, **kwargs)
    		self._connection.commit()
    
    # использование
    db_executor = DBExecutor(host='127.0.0.1', user='root', password='', db='python', charset='utf8mb4', cursorclass=pymysql.cursors.DictCursor, autocommit=True)
    
    
    
    
    
    def create_widgets_in_first_frame():
        # Создать ярлык для рамки
        first_window_label = tkinter.ttk.Label(first_frame, text='Выбор Тары',font=("Helvetica", 18))
        first_window_label.grid(column=0, row=0, pady=10, padx=10, sticky=(tkinter.N))
    #данный код выбирает нажатую вид бутылки и сохраняет данные в этой переменной
       
    
        global var
        var = IntVar()
        var.set(0)
        #t05 = Radiobutton(first_frame,compound='center',  width=55, height=55, text="Тара: 0.5", variable=var, value=0, indicatoron=0).grid(row=0, column=1,pady=20, padx=20)
        #t07 = Radiobutton(first_frame, width=55, height=55, text="Тара: 0.7", variable=var, value=1, indicatoron=0).grid(row=0, column=2,pady=20, padx=20)
    
    
        def quitApp():
            var.set(0)
            first_frame.grid_forget()
            third_frame.grid_forget()
            second_frame.grid(column=0, row=0, padx=20, pady=5, sticky=(tkinter.W, tkinter.N, tkinter.E))
        def quitApp2():
            var.set(1)
            first_frame.grid_forget()
            third_frame.grid_forget()
            second_frame.grid(column=0, row=0, padx=20, pady=5, sticky=(tkinter.W, tkinter.N, tkinter.E))
        global background_img
        global scanBtn_img
        background_img = PhotoImage(file="img/05.gif")
        scanBtn_img = PhotoImage(file="img/07.gif")
    
        background = tkinter.Button(first_frame, image=background_img, command = quitApp).grid(row=7, column=2, padx=30, pady=30)               
        quitButton = tkinter.Button(first_frame, image=scanBtn_img, command = quitApp2).grid(row=7, column=3, padx=30)
        global backgroundimage
        backgroundimage = background_img # сохранить ссылку!
    
    
        # Создать кнопку для рамки
        #first_window_quit_button = tkinter.Button(first_frame, text = "Закрыть", command = quit_program)
        #first_window_quit_button.grid(row=7, column=2, padx=20)
        #first_window_next_button = tkinter.Button(first_frame, text = "Далее", command = call_second_frame_on_top)
        #first_window_next_button.grid(row=7, column=3, padx=20)
    
    def create_widgets_in_second_frame():
        # Create the label for the frame
        second_window_label = tkinter.ttk.Label(second_frame, text='Выбор вида водки')
        second_window_label.grid(column=0, row=0, pady=10, padx=10, sticky=(tkinter.N))
    
        #Второе окно
    
    
        if var.get() == 0:
            listbox_items_05 = ['Айдабульская Люкс', 'Айдабульская Первая', 'Айдабульская Особая',
                                'Айдабульская Наша', 'Айдабульская', 'Айдабульская (голубая)',
                                'Айдабульская  Классическая', 'Айдабульская  Хрустальная',
                                'Айдабульская  Посольская', 'BURABAY глянцевая', 'BURABAY матовая']
    
            def select_item(event):
                global listbox_value_05
                listbox_value_05 = (listbox.get(listbox.curselection()))
    
            listbox_05 = Listbox(second_frame, width=50, height=30, font=('times', 15))
            listbox_05.bind('<<ListboxSelect>>', select_item)
            listbox_05.grid(row=0, column=1, pady=5, padx=5, columnspan=2)
    
            for item in listbox_items_05:
                listbox_05.insert(END, item)
    
        elif var.get() == 1:
            listbox_items_07 = ['Айдабульская Люкс', 'Айдабульская Первая', 'Айдабульская Особая',
                                'Айдабульская Наша', 'Айдабульская', 'Айдабульская (голубая)',
                                'Айдабульская "A"белая  глянцевая', 'Айдабульская "А"черная глянцевая',
                                'Айдабульская  "А"матовая', 'Айдабульская  "А"голубая',
                                'Айдабульская  "А"прозрачная (гол.)', 'Айдабульская  Классическая',
                                'Айдабульская  Хрустальная', 'Айдабульская  Посольская', 'Айдабульская матовая 3D',
                                'Айдабульская матовая Квадрат', 'Айдабульская матовая Премиум',
                                'Айдабульская матовая Степь']
    
            def select_item(event):
                global listbox_value_07
                listbox_value_07 = (listbox.get(listbox.curselection()))
    
            listbox_07 = Listbox(second_frame, width=50, height=30, font=('times', 15))
            listbox_07.bind('<<ListboxSelect>>', select_item)
            listbox_07.grid(row=0, column=1, pady=5, padx=5, columnspan=2)
    
            for item in listbox_items_07:
                listbox_07.insert(END, item)
    
    
        
        
    
    
        # Create the button for the frame
        second_window_back_button = tkinter.Button(second_frame, text = "Назад", width=20, height=6, command = call_first_frame_on_top)
        second_window_back_button.grid(row=7, column=2, padx=20)
        second_window_next_button = tkinter.Button(second_frame, text = "Далее", width=20, height=6, command = call_third_frame_on_top)
        second_window_next_button.grid(row=7, column=3, padx=20)
    
    def create_widgets_in_third_frame():
        # Create the label for the frame
        third_window_label = tkinter.ttk.Label(third_frame)
        third_window_label.grid(column=0, row=0, pady=10, padx=10, sticky=(tkinter.N))
    
        
        def change(event=None):
            if var.get() == 0:
                code_label = code.get()
                company_label = 'Натур продукт'
                country = 'Казахстан'
                time = datetime.strftime(datetime.now(), "%H:%M:%S %d.%m.%Y")
                if len(code.get()) == 0:
                    cmp_txt.insert(END, 'Введите код' + "\n")
                    code_entry.delete(0, END)
                elif len(code.get()) != 0:
                    # Отправка SQL запроса
                    try:
                        db_executor.execute("INSERT INTO `scaner2` (`number`, `tara`, `name_vodka`, `time`, `name_company`, country) VALUES (%s,%s, %s, %s, %s, %s)", (code_label, '0.5', listbox_value, time, company_label, country))
                        print(code.get(), time, company_label, listbox_value)
                        cmp_txt.insert(END, 'Код: ' + code_label + ' Тара: '+'0.5 '+' Название водки: '+ listbox_value + ' Время: ' + time + ' Название компании: ' + company_label + "\n")
                        code_entry.delete(0, END)
                    except pymysql.err.IntegrityError:
                        cmp_txt.insert(END, 'Такое код уже есть в базе' + "\n")
                        code_entry.delete(0, END)
            elif var.get() == 1:
                code_label = code.get()
                company_label = 'Натур продукт'
                country = 'Казахстан'
                time = datetime.strftime(datetime.now(), "%H:%M:%S %d.%m.%Y")
                if len(code.get()) == 0:
                    cmp_txt.insert(END, 'Введите код' + "\n")
                    code_entry.delete(0, END)
                elif len(code.get()) != 0:
                    try:
                        # Отправка SQL запроса
                        db_executor.execute("INSERT INTO `scaner2` (`number`, `tara`, `name_vodka`, `time`, `name_company`, country) VALUES (%s,%s, %s, %s, %s, %s)", (code_label, '0.7', listbox_value, time, company_label, country))
                        print(code.get(), time, company_label)
                        cmp_txt.insert(END, 'Код: ' + code_label + ' Тара: '+'0.7 '+' Название водки: '+ listbox_value + ' Время: ' + time + ' Название компании: ' + company_label + "\n")
                        code_entry.delete(0, END)
                    except pymysql.err.IntegrityError:
                        cmp_txt.insert(END, 'Такое код уже есть в базе' + "\n")
                        code_entry.delete(0, END)
    
    
        code = StringVar()
        code_label = Label(third_frame,text="Введите штрихкод:").grid(row=0, column=0, sticky=W, pady=10, padx=10)
        code_entry = Entry(third_frame,textvariable=code)
        code_entry.bind('<Return>', change)
        code_entry.focus_set()
        code_entry.grid(row=0, column=1, columnspan=2,  sticky=W+E, padx=10)
    
        
    
        cmp_txt = Text(third_frame, width=123, height=50)
        cmp_txt.grid(row=4, column=1, columnspan=2)
        scroll = Scrollbar(command=cmp_txt.yview)
     
        cmp_txt.config(yscrollcommand=scroll.set)
        button = Button(third_frame,text="Отправить", width=20, height=6, command=change).grid(row=7, column=3, padx=20)
    
    
    
    
    
    
    
    
    
    
        # Create the button for the frame
        third_window_back_button = tkinter.Button(third_frame, text = "Назад", width=20, height=6, command = call_second_frame_on_top)
        third_window_back_button.grid(row=7, column=1,pady=20, padx=20)
        
    def call_first_frame_on_top():
        # This function can be called only from the second window.
        # Hide the second window and show the first window.
        second_frame.grid_forget()
        first_frame.grid(column=0, row=0, padx=20, pady=5, sticky=(tkinter.W, tkinter.N, tkinter.E))
    
    def call_second_frame_on_top():
        # This function can be called from the first and third windows.
        # Hide the first and third windows and show the second window.
        first_frame.grid_forget()
        third_frame.grid_forget()
        second_frame.grid(column=0, row=0, padx=20, pady=5, sticky=(tkinter.W, tkinter.N, tkinter.E))
    
    def call_third_frame_on_top():
        # This function can only be called from the second window.
        # Hide the second window and show the third window.
        second_frame.grid_forget()
        third_frame.grid(column=0, row=0, padx=20, pady=5, sticky=(tkinter.W, tkinter.N, tkinter.E))
    
    def quit_program():
        root_window.destroy()
    
    ###############################
    # Main program starts here :) #
    ###############################
    
    # Создать корневое окно графического интерфейса.
    root_window = tkinter.Tk()
    root_window.geometry('1200x800')
    root_window.title('Считыватель Штрих кодов')
    # Определить размер окна
    window_width = 1200
    window_heigth = 800
    
    
    # Создайте фреймы внутри корневого окна для хранения других элементов графического интерфейса. Все кадры должны быть созданы в основной программе, иначе они не доступны в функциях. 
    first_frame=tkinter.ttk.Frame(root_window, width=window_width, height=window_heigth)
    first_frame['borderwidth'] = 2
    first_frame['relief'] = 'sunken'
    first_frame.grid(column=0, row=0, padx=20, pady=5)
    
    second_frame=tkinter.ttk.Frame(root_window, width=600, height=600)
    second_frame['borderwidth'] = 2
    second_frame['relief'] = 'sunken'
    second_frame.grid(column=0, row=0, padx=20, pady=5, sticky=(tkinter.W, tkinter.N, tkinter.E))
    
    third_frame=tkinter.ttk.Frame(root_window, width=window_width, height=window_heigth)
    third_frame['borderwidth'] = 2
    third_frame['relief'] = 'sunken'
    third_frame.grid(column=0, row=0, padx=20, pady=5, sticky=(tkinter.W, tkinter.N, tkinter.E))
    
    # Create all widgets to all frames
    create_widgets_in_third_frame()
    create_widgets_in_second_frame()
    create_widgets_in_first_frame()
    
    # Скрыть все кадры в обратном порядке, но оставить первый кадр видимым (невидимым).
    third_frame.grid_forget()
    second_frame.grid_forget()
    
    # Start tkinter event - loop
    root_window.mainloop()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

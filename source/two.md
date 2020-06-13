---
title: two
date: 2020-05-07
---
Example Python program two.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import pymysql.cursors
* import pymysqlpool
* from tkinter import *
* from datetime import datetime
* import tkinter.ttk

## Classes

* class DBExecutor():

## Methods

* 	def __init__(self, **connection_params):
* 	def _connect(self):
* 	def execute(self, sql, *args, **kwargs):
* def create_widgets_in_first_frame():
* def create_widgets_in_second_frame():
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
        first_window_label = tkinter.ttk.Label(first_frame, text='Выбор Тары')
        first_window_label.grid(column=0, row=0, pady=10, padx=10, sticky=(tkinter.N))
    #данный код выбирает нажатую вид бутылки и сохраняет данные в этой переменной
       
    
        global var
        var = IntVar()
        var.set(0)
        t05 = Radiobutton(first_frame,text="Тара: 0.5", variable=var, value=0, indicatoron=0).grid(row=0, column=1,pady=20, padx=20)
        t07 = Radiobutton(first_frame,text="Тара: 0.7", variable=var, value=1, indicatoron=0).grid(row=0, column=2,pady=20, padx=20)
    
    
    
        # Создать кнопку для рамки
        first_window_quit_button = tkinter.Button(first_frame, text = "Закрыть", command = quit_program)
        first_window_quit_button.grid(row=1, column=1,pady=20, padx=20)
        first_window_next_button = tkinter.Button(first_frame, text = "Далее", command = call_second_frame_on_top)
        first_window_next_button.grid(row=1, column=2,pady=20, padx=20)
    
    def create_widgets_in_second_frame():
        # Create the label for the frame
        second_window_label = tkinter.ttk.Label(second_frame, text='Window 2')
        second_window_label.grid(column=0, row=0, pady=10, padx=10, sticky=(tkinter.N))
    
    
    
        #Второе окно
     
    
    
    
    
    
    
        # Create the button for the frame
        second_window_back_button = tkinter.Button(second_frame, text = "Назад", command = call_first_frame_on_top)
        second_window_back_button.grid(row=1, column=1,pady=20, padx=20)
        second_window_next_button = tkinter.Button(second_frame, text = "Далее", command = call_third_frame_on_top)
        second_window_next_button.grid(row=1, column=2,pady=20, padx=20)
    
    def create_widgets_in_third_frame():
        # Create the label for the frame
        third_window_label = tkinter.ttk.Label(third_frame, text='Window 3')
        third_window_label.grid(column=0, row=0, pady=10, padx=10, sticky=(tkinter.N))
        
        def change(event=None):
            if var.get() == 0:
                code_label = code.get()
                company_label = 'Натур продукт'
                time = datetime.strftime(datetime.now(), "%H:%M:%S %d.%m.%Y")
                third_frame.bind('<Return>', change)
                if len(code.get()) == 0:
                    cmp_txt.insert(END, 'Введите код' + "\n")
                    code_entry.delete(0, END)
                elif len(code.get()) != 0:
                    # Отправка SQL запроса
                    db_executor.execute("INSERT INTO `scaner` (`number`, `tara`, `time`, `name_company`) VALUES (%s, %s, %s, %s)", (code_label, '0.5', time, company_label))
                    print(code.get(), time, company_label)
                    cmp_txt.insert(END, 'Код: ' + code_label + ' Тара: '+'0.5 '+ 'Время: ' + time + ' Название компании: ' + company_label + "\n")
                    code_entry.delete(0, END)
            elif var.get() == 1:
                code_label = code.get()
                company_label = 'Натур продукт'
                time = datetime.strftime(datetime.now(), "%H:%M:%S %d.%m.%Y")
                third_frame.bind('<Return>', change)
                if len(code.get()) == 1:
                    cmp_txt.insert(END, 'Введите код' + "\n")
                    code_entry.delete(0, END)
                elif len(code.get()) != 0:
                    # Отправка SQL запроса
                    db_executor.execute("INSERT INTO `scaner` (`number`, `tara`, `time`, `name_company`) VALUES (%s, %s, %s, %s)", (code_label, '0.7', time, company_label))
                    print(code.get(), time, company_label)
                    cmp_txt.insert(END, 'Код: ' + code_label + ' Тара: '+'0.7 '+ 'Время: ' + time + ' Название компании: ' + company_label + "\n")
                    code_entry.delete(0, END)	
    
    
        code = StringVar()
        code_label = Label(third_frame,text="Введите штрихкод:").grid(row=0, column=0, sticky=W, pady=10, padx=10)
        code_entry = Entry(third_frame,textvariable=code)
        code_entry.focus_set()
        code_entry.grid(row=0, column=1, columnspan=2,  sticky=W+E, padx=10)
        cmp_txt = Text(third_frame, height=11)
        cmp_txt.grid(row=4, column=1, columnspan=2)
    
        button = Button(third_frame,text="Отправить", command=change).grid(row=1, column=2, padx=20)
    
    
    
    
    
    
    
    
    
    
        # Create the button for the frame
        third_window_back_button = tkinter.Button(third_frame, text = "Назад", command = call_second_frame_on_top)
        third_window_back_button.grid(row=1, column=1,pady=20, padx=20)
        
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
    # Определить размер окна
    window_width = 500
    window_heigth = 600
    
    
    # Создайте фреймы внутри корневого окна для хранения других элементов графического интерфейса. Все кадры должны быть созданы в основной программе, иначе они не доступны в функциях. 
    first_frame=tkinter.ttk.Frame(root_window, width=window_width, height=window_heigth)
    first_frame['borderwidth'] = 2
    first_frame['relief'] = 'sunken'
    first_frame.grid(column=0, row=0, padx=20, pady=5)
    
    second_frame=tkinter.ttk.Frame(root_window, width=window_width, height=window_heigth)
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

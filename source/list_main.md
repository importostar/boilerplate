---
title: list_main
date: 2020-05-07
---
Example Python program list_main.py

## Modules

* from tkinter import *
* from tkinter import ttk
* from tkinter import messagebox

## Methods

* def delete():
* def add():

## Code

Python tkinter example

    from tkinter import *
    from tkinter import ttk
    from tkinter import messagebox
    
    
    # удаление выделенного элемента
    def delete():
        selection = languages_listbox.curselection()  # получение выбраного элемента
        mes = messagebox.askyesno(title="Вопрос", message="Удалить данные?")  # вопрос об удалении
        if mes == TRUE: # удаление этого элемента
            languages_listbox.delete(selection[0])
    
    
    # добавление нового элемента
    def add():
        new_language = language_entry.get()  # получение информации из поля entry
        languages_listbox.insert(0, new_language)  # вывод в listbox
        writer = open('language.txt', 'a')
        writer.write(' ' + str(new_language))
        writer.close()
    
    
    root = Tk()
    root.title("GUI на Python")
    
    # текстовое поле и кнопка для добавления в список
    language_entry = Entry(width=40)  # размер поля ввода
    language_entry.grid(column=0, row=0, padx=6, pady=6)
    add_button = ttk.Button(text="Добавить", command=add).grid(column=1, row=0, padx=6, pady=6)
    
    # создаем список
    languages_listbox = Listbox()
    languages_listbox.grid(row=1, column=0, columnspan=2, sticky=W + E, padx=5, pady=5)
    
    # добавляем в список начальные элементы
    
    writer = open('language.txt', 'a')
    writer.write(' ')
    writer = open('language.txt')
    for line in writer:
        words = line.split()
    for i in range(len(words)):
        languages_listbox.insert(END,words[i])
    writer.close()
    
    delete_button = ttk.Button(text="Удалить", command=delete).grid(row=2, column=1, padx=5, pady=5)
    
    root.mainloop()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

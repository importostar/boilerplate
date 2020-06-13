---
title: qtablewidget example
date: 2020-05-07
---
Example Python program qtablewidget-example.py
This program creates a PyQt GUI
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import sys
* from functools import partial
* from PyQt5.QtCore import Qt
* from PyQt5.QtWidgets import QApplication, QWidget, QTableWidget, QTableWidgetItem, QVBoxLayout, QPushButton, QCheckBox

## Classes

* class MainWindow(QWidget):

## Methods

* def __init__(self):
* def prepare_table(self):
* def fill_table(self):
* def item_changed(self, item):
* def cell_changed(self, row, col):
* def button_clicked(self, person):
* def keyPressEvent(self, event):

## Code

Example Python PyQt program :

    import sys
    from functools import partial
    
    from PyQt5.QtCore import Qt
    from PyQt5.QtWidgets import QApplication, QWidget, QTableWidget, QTableWidgetItem, QVBoxLayout, QPushButton, QCheckBox
    
    
    class MainWindow(QWidget):
        def __init__(self):
            # Инициализируем приложение
            super().__init__()
            self.setWindowTitle('Table Example')
            self.resize(600, 600)
            self.layout = QVBoxLayout(self)
            self.setLayout(self.layout)
            self.table = QTableWidget(self)
            self.layout.addWidget(self.table)
            # Делаем так, чтобы выделялась не ячейка, а строка
            self.table.setSelectionBehavior(QTableWidget.SelectRows)
            # Данные - список людей
            self.persons = [
                [0, 'Вася', 'Васильев'],
                [1, 'Петя', 'Петров'],
                [2, 'Иван', 'Иванов'],
            ]
            # Готовим таблицу, добавляем заголовки
            self.prepare_table()
            # Заполняем таблицу данными
            self.fill_table()
            # Изменени ячейки (вариант 1)
            self.table.itemChanged.connect(self.item_changed)
            # Изменени ячейки (вариант 2)
            self.table.cellChanged.connect(self.cell_changed)
    
        def prepare_table(self):
            self.table.setColumnCount(4)
            self.table.setHorizontalHeaderLabels(['ID', 'Имя', 'Фамилия', 'Widget 1'])
    
        def fill_table(self):
            for (row, person) in enumerate(self.persons):
                # Вставляем строчку
                self.table.insertRow(row)
    
                # Добавляем нередактируемую ячейку с ID
                item = QTableWidgetItem(str(person[0]))
                item.setFlags(Qt.ItemIsEnabled)
                self.table.setItem(row, 0, item)
    
                # Добавляем ячейки с именем и фамилией
                item = QTableWidgetItem(person[1])
                # Чтобы не искать, на какого пользователя нажали, можно привязать к ячейке данные
                # (!) но это необязательно, мы это не будем использовать (!)
                # UserRole - это назначение данных
                item.setData(Qt.UserRole, person) # (!)
                self.table.setItem(row, 1, item)
    
                item = QTableWidgetItem(person[2])
                # Чтобы не искать, на какого пользователя нажали, можно привязать к ячейке данные
                # (!) но это необязательно, мы это не будем использовать
                item.setData(Qt.UserRole, person) # (!)
                self.table.setItem(row, 2, item)
    
                # Добавляем ячейку с виджетом внутри
                # В качестве примера -- кнопка, но тут могут быть и почти любые другие виджеты
                # Родитель -- таблица
                button = QPushButton(self.table)
                button.setText('Кнопка #' + str(person[0]))
                # Надо знать, на какую именно кнопку нажали
                # Используем functools.partial, чтобы передать функцию, которая вызовет нашу функцию с параметром
                button.clicked.connect(partial(self.button_clicked, person))
                # Добавляем кнопку через setCellWidget вместо setItem
                self.table.setCellWidget(row, 3, button)
                # Например, это могла быть кнопка для удаления или редактирования.
                # Или тут мог быть CheckBox
                # Или Combobox, SpinBox и т.д.
    
        def item_changed(self, item):
            # Определяем, в какой строке изменение
            row = item.row()
            # Определяем, что это за человек.
            # Если данные фильтруются или сортируются, это может быть более сложное действие
            person = self.persons[row]
            # Меняем данные в источнике данных
            person[item.column()] = item.text()
            # Выводим всё, чтобы проверить
            print(self.persons)
    
            # Но мы могли взять пользователя и из данных (!)
            # Обратите внимание, тут неизменённый пользователь, потому что это копия (!)
            print(item.data(Qt.UserRole))
    
        def cell_changed(self, row, col):
            # Метод похож на itemChanegd, но в параметрах позиция ячейки, а не сам item
            print(f'Cell Changed {row} : {col}')
    
        def button_clicked(self, person):
            print('Нажата кнопка на человеке: ', person)
    
        def keyPressEvent(self, event):
            if event.key() == Qt.Key_Delete:
                print('Delete pressed')
                # Получаем все выделенные ячейки
                items = self.table.selectedItems()
                # А потом из ячеек выделенные строки (с множеством, чтобы без повторений)
                rows = list(set([item.row() for item in items]))
                print('Rows to delete: ', rows)
                # Но удалять по индексам мы не можем
                # потому что после удаления одной строчки, остальные сдвинутся, и номера строк уже будут неактуальными
                # решение очень простое - отсортируем их в обратном порядке, чтобы удалять с конца, тогда сдвигов не будет
                rows = reversed(sorted(rows))
                for row in rows:
                    # Удаляем человека
                    del self.persons[row]
                    # Удаляем строчка
                    self.table.removeRow(row)
                # Проверка
                print(self.persons)
    
                '''
                Тут было простое удаление, потому что номер строчки в таблице совпадал с номером человека в списке.
                Если бы это было не так (например, мы их выводили отсортированно или фильтровано или ещё что-нибудь),
                то пришлось бы вручную искать каждого человека для удаления.
                
                Иногда проще просто заново собрать всю табличку
                '''
    
    
    if __name__ == '__main__':
        app = QApplication(sys.argv)
        mainForm = MainWindow()
        mainForm.show()
        sys.exit(app.exec())
    

## Useful Links

- Articles: https://python-commandments.org/
- PyQt: https://pythonpyqt.com/

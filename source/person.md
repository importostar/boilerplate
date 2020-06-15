---
title: person
date: 2020-05-07
---
Example Python program person.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import shelve
* import tkinter
* import tkinter.messagebox

## Classes

* class Person:
* class Manager(Person):
* class PersonCUI:
* class PersonGUI(tkinter.Frame):

## Methods

* def __init__(self, name, age, pay=0, job=None):
* def __str__(self):
* def last_name(self):
* def give_raise(self, percent):
* def key(self):
* def save_to(self, shelve_name):
* def save(self):
* def load_from(cls, shelve_name, key):
* def load(cls, key):
* def __init__(self, name, age, pay, employees=2):
* def give_raise(self, percent, bonus):
* def start(self):
* def __init__(self, parent=None):
* def fetch(self, key):
* def update(self, key):

## Code

Python tkinter example

    #!/usr/local/bin/python3
    
    """
    Implementation of persons for a pim database
    """
    
    import shelve
    import tkinter
    import tkinter.messagebox
    
    
    DEFAULT_SHELVE_NAME = 'people'
    
    
    class Person:
        """
        gerneral Person class
        """
    
        def __init__(self, name, age, pay=0, job=None):
            self.name = name
            self.age = age
            self.pay = pay
            self.job = job
    
        def __str__(self):
            properties = []
            for prop in self.__dict__:
                properties.append('%s: %s' % (prop, self.__dict__[prop]))
            return ('<%s => %s>' %
                    (self.__class__.__name__, '; '.join(properties)))
    
        def last_name(self):
            return name.split()[-1]
    
        def give_raise(self, percent):
            self.pay *= (1.0 + percent)
    
        def key(self):
            return self.name.replace(' ', '_')
    
        def save_to(self, shelve_name):
            db = shelve.open(shelve_name)
            db[self.key()] = self
            db.close()
    
        def save(self):
            self.save_to(DEFAULT_SHELVE_NAME)
    
        @classmethod
        def load_from(cls, shelve_name, key):
            db = shelve.open(shelve_name)
            result = db[key]
            db.close()
            return result
    
        @classmethod
        def load(cls, key):
            return cls.load_from(DEFAULT_SHELVE_NAME, key)
    
    
    class Manager(Person):
        """
        Manager class that has special give_raise method
        """
    
        def __init__(self, name, age, pay, employees=2):
            Person.__init__(self, name, age, pay, 'manager')
            self.employees = employees
    
        def give_raise(self, percent, bonus):
            Person.give_raise(self, percent + bonus)
    
    
    class PersonCUI:
        """
        console interface for persons
        """
    
        def start(self):
            while True:
                key = input('\nkey? => ')
                if not key:
                    break
                try:
                    record = Person.load(key)
                except:
                    print('No such key "%s"!' % key)
                else:
                    for field in record.__dict__.keys():
                        current_value = getattr(record, field)
                        new_value = input('\t[%s]=%s\n\tnew?=>' %
                                            (field, current_value))
                        if new_value:
                            setattr(record, field, eval(new_value))
                    record.save()
    
    
    class PersonGUI(tkinter.Frame):
        """
        graphical interface for persons
        """
    
        def __init__(self, parent=None):
            tkinter.Frame.__init__(self, parent)
            self.form = tkinter.Frame(self)
            self.entries = {}
            self.key_list = tkinter.Listbox(self)
            self.key_list.insert(0, 'NEW')
            db = shelve.open(DEFAULT_SHELVE_NAME)
            for key in db.keys():
                self.key_list.insert(tkinter.END, key)
            self.key_list.pack(side=tkinter.TOP)
            for (idx, string_label) in enumerate(Person('?', 0).__dict__.keys()):
                label = tkinter.Label(self.form, text=string_label)
                entry = tkinter.Entry(self.form)
                label.grid(row=idx, column=0)
                entry.grid(row=idx, column=1)
                self.entries[string_label] = entry
            fetch_button = tkinter.Button(self, text='Fetch',
                                          command=(lambda: self.fetch(
                                                    self.key_list.get(self.key_list.curselection()))))
            update_button = tkinter.Button(self, text='Update',
                                           command=(lambda: self.update(
                                                    self.key_list.get(self.key_list.curselection()))))
            self.form.pack()
            fetch_button.pack(side=tkinter.LEFT)
            update_button.pack(side=tkinter.LEFT)
    
        def fetch(self, key):
            try:
                record = Person.load(key)
            except:
                tkinter.messagebox.showerror(title='Error!',
                                             message='No such key "%s"!' % key)
            else:
                for field in record.__dict__.keys():
                    self.entries[field].delete(0, tkinter.END)
                    self.entries[field].insert(0, repr(getattr(record, field)))
    
        def update(self, key):
            new = False
            try:
                record = Person.load(key)
            except:
                record = Person('?', 0)
                new = True
            for field in record.__dict__.keys():
                setattr(record, field, eval(self.entries[field].get()))
            if new:
                self.key_list.insert(tkinter.END, record.key())
            record.save()
    
    
    if __name__ == '__main__':
        #PersonCUI().start()
        window = tkinter.Tk()
        window.title('PeopleDB')
        form = PersonGUI(window)
        form.pack()
        window.mainloop()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

---
title: bankingsystem
date: 2020-05-07
---
Example Python program bankingsystem.py

## Modules

* import tkinter as tk
* from tkinter import messagebox
* from tkinter import simpledialog

## Classes

* class BankAccount(object):

## Methods

* def __init__(self, name, initial_balance=0):
* def deposit(self, amount):
* def withdraw(self, amount): 
* def overdrawn(self):
* def cur_account():
* def depositCallback():
* def withdrawCallback():
* def checkCallBack():

## Code

Python tkinter example

    import tkinter as tk
    from tkinter import messagebox
    from tkinter import simpledialog
    
    root = tk.Tk()
    
    mensen = ['Hugo', 'Floris', 'Koen', 'Tim', 'Tristan', 'Soufian']
    
    class BankAccount(object):
        def __init__(self, name, initial_balance=0):
            self. name =  name
            self.balance = initial_balance
            
        def deposit(self, amount):
            if (amount >=0):
                self.balance += amount
            else:
                messagebox.showerror("sorry foutje", "amount must be bigger than 0") #ik kom op sorry foutje door een kassa die gaf die error niet dat ik zelf zoiets doms bedenk ik vond het wel grappig
            
        def withdraw(self, amount): 
            if (amount >=0):
                self.balance -= amount
            else:
                messagebox.showerror("sorry foutje", "amount must be bigger than 0")
    
        def overdrawn(self):
            return self.balance < 0
    
    accounts = [BankAccount(mens) for mens in mensen]
    
    def cur_account():
      i, = Lb1.curselection()
      return accounts[i]
    
    def depositCallback():
      amount = simpledialog.askinteger("deposit", "How many dollars?")
      cur_account().deposit(amount)
    
    def withdrawCallback():
      amount = simpledialog.askinteger("withdraw", "How many dollars")
      cur_account().withdraw(amount)
    
    def checkCallBack():
      messagebox.showinfo( "balance", f'{cur_account(). name} has {cur_account().balance} dollars')
    
    root.title("ReAlbankNoScAm")
    
    Lb1 = tk.Listbox(root)
    for i, account in enumerate(accounts):
      Lb1.insert(i, account.name)
    Lb1.pack()
    
    ButtonDeposit = tk.Button(root, text="deposit", command=depositCallback)
    ButtonDeposit.pack()
    
    ButtonWithdraw = tk.Button(root, text="withdraw", command=withdrawCallback)
    ButtonWithdraw.pack()
    
    ButtonCheck = tk.Button(root, text="check", command=checkCallBack)
    ButtonCheck.pack()
    
    root.mainloop()
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

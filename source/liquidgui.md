---
title: liquidgui
date: 2020-05-07
---
Example Python program liquidgui.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import tkinter
* from tkinter import *
* from tkinter import font
* from tkinter import ttk
* from quoine.client import Quoinex
* import datetime
* import time
* import urllib
* import json
* import requests
* import pprint

## Methods

* def main():
* def info():
* def limit_buy(quantity,price):
* def market_buy(quantity):
* def limit_sell(quantity,price):
* def market_sell(quantity):
* def cancel(id):
* def update(id,quantity,price):#未約定の注文の変更
* def update_t(id,stop_loss,take_profit):#約定済の注文の変更
* def close(id):#約定済の注文を成り行きでクローズ
* def button1_clicked():
* def button2_clicked():
* def button3_clicked():

## Code

Python tkinter example

    import tkinter
    from tkinter import *
    from tkinter import font
    from tkinter import ttk
    from quoine.client import Quoinex
    import datetime
    import time
    import urllib
    import json
    import requests
    import pprint
    
    
    def main():
        q = Quoinex('ID', 'SECRET')
    
        def info():
            #balance = q.get_account_balances() #残高
            #depth = q.get_order_book(product_id=5)  #板の取得。BTC/JPYのIDは5
            trades = q.get_trades(limit=1).get('models')
            orders = q.get_orders(limit=1).get('models')
            #print(trades)
            #print(orders)
            if trades[0].get('status') == 'open':
                global tid,side
                tid = trades[0].get('id')
                side = trades[0].get('side')
            else:
                side = 'flat'
            return trades,orders,side
    
        def limit_buy(quantity,price):
            callback = q.create_margin_order(order_type=Quoinex.ORDER_TYPE_LIMIT,product_id=5,leverage_level=25,side=Quoinex.SIDE_BUY,quantity=quantity,price=price,order_direction='netout')
            #print(callback)
            id = callback.get('id')
            text1.configure(state='normal')
            text1.insert('end',str(callback)+'\n')
            text1.yview(END)
            text1.configure(state='disabled')
    
        def market_buy(quantity):
            callback = q.create_margin_order(order_type=Quoinex.ORDER_TYPE_MARKET,product_id=5,leverage_level=25,side=Quoinex.SIDE_BUY,quantity=quantity,price=None,order_direction='netout')
            #print(callback)
            id = callback.get('id')
            text1.configure(state='normal')
            text1.insert('end',str(callback)+'\n')
            text1.yview(END)
            text1.configure(state='disabled')
    
        def limit_sell(quantity,price):
            callback = q.create_margin_order(order_type=Quoinex.ORDER_TYPE_LIMIT,product_id=5,leverage_level=25,side=Quoinex.SIDE_SELL,quantity=quantity,price=price,order_direction='netout')
            #print(callback)
            id = callback.get('id')
            text1.configure(state='normal')
            text1.insert('end',str(callback)+'\n')
            text1.yview(END)
            text1.configure(state='disabled')
    
        def market_sell(quantity):
            callback = q.create_margin_order(order_type=Quoinex.ORDER_TYPE_MARKET,product_id=5,leverage_level=25,side=Quoinex.SIDE_SELL,quantity=quantity,price=None,order_direction='netout')
            #print(callback)
            id = callback.get('id')
            text1.configure(state='normal')
            text1.insert('end', str(callback)+'\n')
            text1.yview(END)
            text1.configure(state='disabled')
    
        def cancel(id):
            callback = q.cancel_order(order_id=id)
            #print(callback) 
    
        def update(id,quantity,price):    #未約定の注文の変更
            callback = q.update_live_order(order_id=id, quantity=quantity, price=price)
            #print(callback)   
    
        def update_t(id,stop_loss,take_profit):    #約定済の注文の変更
            callback = q.update_trade(trade_id=id, stop_loss=stop_loss, take_profit=take_profit)
            #print(callback)
    
        def close(id):    #約定済の注文を成り行きでクローズ
            callback = q.close_trade(trade_id=id)  
            text1.configure(state='normal')
            text1.insert('end',str(callback)+'\n')
            text1.yview(END)
            text1.configure(state='disabled')  
            #print(callback)
    
        trades = info()[0]
        orders = info()[1]
        def button1_clicked():
            price = entry1.get()
            size = entry2.get()
            if not price:
                market_buy(size)
                time.sleep(0.1)
                trades = info()[0]
                orders = info()[1]
                side = info()[2]
                label1.configure(text='Balance:'+str(round(float(balance))))
                label2.configure(text='Side:'+side)
            else:
                limit_buy(size, price)
                time.sleep(0.1)
                trades = info()[0]
                orders = info()[1]
                side = info()[2]
                label1.configure(text='Balance:'+str(round(float(balance))))
                label2.configure(text='Side:'+side)
    
        def button2_clicked():
            price = entry1.get()
            size = entry2.get()
            if not price:
                market_sell(size)
                time.sleep(0.1)
                trades = info()[0]
                orders = info()[1]
                side = info()[2]
                label1.configure(text='Balance:'+str(round(float(balance))))
                label2.configure(text='Side:'+side)            
            else:
                limit_sell(size, price) 
                time.sleep(0.1)
                trades = info()[0]
                orders = info()[1]
                side = info()[2]
                label1.configure(text='Balance:'+str(round(float(balance))))
                label2.configure(text='Side:'+side)
        def button3_clicked():    
            close(tid)
            time.sleep(0.1)            
            trades = info()[0]
            orders = info()[1]
            side = info()[2]
            label1.configure(text='Balance:'+str(round(float(balance))))
            label2.configure(text='Side:'+side)
    
    
        if trades[0].get('status') == 'open':
            global tid,side
            tid = trades[0].get('id')
            side = trades[0].get('side')
        else:
            side = 'flat'
        if orders[0].get('status') == 'live':
            oid = orders[0].get('id') 
        else:
            pass
        balances = q.get_account_balances() #JPYが辞書イン辞書の何番目か定かでないので探す
        for i in range(len(balances)):
            if balances[i].get('currency') == 'JPY':
                balance = balances[i].get('balance')
            else:
                pass
        root = tkinter.Tk()
        root.title('Liquid Oeder Client v1.00')
        root.geometry('320x280')
        label1 = tkinter.Label(root, text='Balance:'+str(round(float(balance))))
        label1.grid(row=1, sticky='w')
        label2 = tkinter.Label(root, text='Side:'+side)
        label2.grid(row=2, sticky='w')
        label3 = tkinter.Label(root, text='Price')
        label3.grid(row=3, column=0)
        label4 = tkinter.Label(root, text='Size') 
        label4.grid(row=3, column=1)
        entry1 = tkinter.Entry(root,font=('',12),justify='center',width=15)
        entry1.grid(row=4, column=0)
        entry2 = tkinter.Entry(root,font=('',12),justify='center',width=15)
        entry2.grid(row=4, column=1)
        button1 = tkinter.Button(text='LONG',command=button1_clicked,width=20,height=5,fg='green')  
        button1.grid(row=5,column=0,sticky='ns')
        button2 = tkinter.Button(text='SHORT',command=button2_clicked,width=20,height=5,fg='red')  
        button2.grid(row=5,column=1,sticky='ns') 
        button3 = tkinter.Button(text='CLOSE',command=button3_clicked,width=20,height=5,fg='blue')
        button3.grid(row=6,column=0,sticky='nsew') 
        text1 = tkinter.Text(height=5,width=5)
        text1.grid(row=6,column=1,ipadx=55,sticky='nsew',columnspan=2) 
        text1.configure(state='disabled')
        scrollbar = ttk.Scrollbar(
            root, 
            orient=VERTICAL, 
            command=text1.yview)
        text1['yscrollcommand'] = scrollbar.set
        scrollbar.grid(row=6,column=3,sticky='ns')
        root.mainloop()
    
    if __name__ == '__main__':
        main()    
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

---
title: Fingerchess
date: 2020-05-07
---
Example Python program Fingerchess.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import socket
* import sys
* import time
* import os
* import tkinter.messagebox
* from tkinter import *

## Methods

* def serverConn():
* def sendCl():
* def clientConn():

## Code

Python tkinter example

    import socket
    import sys
    import time
    import os
    import tkinter.messagebox
    from tkinter import *
    
    #SAVE AS .pyw TO HIDE CMD
    BUFSIZ=1024
    serverLeft=1
    serverRight=1
    clientLeft=1
    clientRight=1
    scoreServer=0
    scoreClient=0
    msg=''
    
    root=Tk()
    
    #def zero Down
                
    def serverConn():
        global serverLeft
        global serverRight
        global clientLeft
        global clientRight
        global msg
        host = socket.gethostname()
        s = socket.socket()
        port = 8080
        s.bind((host,port))
        print("Server done binding to host and port successfully")
        print("Server is waiting for incoming connections")
        s.listen(5)
        conn, addr = s.accept()
        print(addr, "Has connected to the server and is now online")
        for connButton in root.grid_slaves():
            if int(connButton.grid_info()["row"])==4:
                connButton.grid_forget()
        #Enemy Entries
        enemyLText="Enemy left fingers:"
        enemyLLabel=Label(root, text=enemyLText)
        enemyLLabel.grid(row=1, column=1)
        enemyLEntry=Entry(root)
        enemyLEntry.insert(0, clientLeft)
        enemyLEntry.grid(row=1, column=2)
        enemyRText="Enemy right fingers:"
        enemyRLabel=Label(root, text=enemyRText)
        enemyRLabel.grid(row=1, column=3)        
        enemyREntry=Entry(root)
        enemyREntry.insert(0, clientRight)
        enemyREntry.grid(row=1, column=4)
        
        #Your Entries
        yourLText="Your left fingers:"
        yourLLabel=Label(root, text=yourLText).grid(row=2, column=1)
        yourLEntry=Entry(root)
        yourLEntry.insert(0, serverLeft)
        yourLEntry.grid(row=2, column=2)
        yourRText="Your right fingers:"
        yourRLabel=Label(root, text=yourRText)
        yourRLabel.grid(row=2, column=3)
        yourREntry=Entry(root)
        yourREntry.insert(0, serverRight)
        yourREntry.grid(row=2, column=4)
        incoming_message = conn.recv(1024)
        incoming_message = incoming_message.decode()
        print("Server: ", incoming_message)
        if incoming_message=="L to R":
            serverRight=serverRight+clientLeft
            if serverRight==6:
                serverRight=1
            elif serverRight==7:
                serverRight=2
            elif serverRight==8:
                serverRight=3
            elif serverRight==9:
                serverRight=4
        elif incoming_message=="L to L":
            serverLeft=serverLeft+clientLeft  
            if serverLeft==6:
                serverLeft=1
            elif serverLeft==7:
                serverLeft=2
            elif serverLeft==8:
                serverLeft=3
            elif serverLeft==9:
                serverLeft=4                        
        elif incoming_message=="R to R":
            serverRight=serverRight+clientRight  
            if serverRight==6:
                serverRight=1
            elif serverRight==7:
                serverRight=2
            elif serverRight==8:
                serverRight=3
            elif serverRight==9:
                serverRight=4
        elif incoming_message=="R to L":
            serverLeft=serverLeft+clientRight
            if serverLeft==6:
                serverLeft=1
            elif serverLeft==7:
                serverLeft=2
            elif serverLeft==8:
                serverLeft=3
            elif serverLeft==9:
                serverLeft=4
        
        #Resolving Attacks
    def sendCl():
        global msg
        msg = messageCMove.get()
        messageCMove.set("")
        print(msg)
        print("hi")
               
    def clientConn():
        global serverLeft
        global serverRight
        global clientLeft
        global clientRight
        global conn
        global msg
        s=socket.socket()
        host=hostEntry.get()
        port=8080
        s.connect((host,port))
        print("Connected")
        for cliButton in root.grid_slaves():
            if int(cliButton.grid_info()["row"])==4:
                cliButton.grid_forget()
        for cliLabel1 in root.grid_slaves():
            if int(cliLabel1.grid_info()["row"])==2:
                cliLabel1.grid_forget()
        for cliLabel2 in root.grid_slaves():
            if int(cliLabel2.grid_info()["row"])==3:
                cliLabel2.grid_forget()
                
        clientAttack=StringVar()
        entry_field=Entry(root, textvariable=clientAttack)
        entry_field.grid(row=3, column=1)
        clientAttack.set("Type your move")
        messageCMove=clientAttack.get()
        attkClientButton=Button(root, text="Attack!", command=sendCl)
        attkClientButton.grid(row=6, column=1)
        clientAttack.set("")
        message = messageCMove
        if message=="L to R":
             if clientLeft==0:
               fingers=False
               while (fingers==False):
                   message=input(str("You cannot attack with a hand that has 0 fingers. Enter your move: "))
                   if (message!="L to R" and message!="L to L"):
                       fingers=True
             serverRight=serverRight+clientLeft
             if serverRight==6:
                 serverRight=1
             elif serverRight==7:
                 serverRight=2
             elif serverRight==8:
                 serverRight=3
             elif serverRight==9:
                 serverRight=4
        elif message=="L to L":
            if clientLeft==0:
                fingers=False
                while (fingers==False):
                    message=input(str("You cannot attack with a hand that has 0 fingers. Enter your move: "))
                    if (message!="L to R" and message!="L to L"):
                        fingers=True
            serverLeft=serverLeft+clientLeft
            if serverLeft==6:
                serverLeft=1
            elif serverLeft==7:
                serverLeft=2
            elif serverLeft==8:
                serverLeft=3
            elif serverLeft==9:
                serverLeft=4
        elif message=="R to R":
            if clientRight==0:
                fingers=False
                while (fingers==False):
                    message=input(str("You cannot attack with a hand that has 0 fingers. Enter your move: "))
                    if (message!="R to R" and message!="R to L"):
                        fingers=True
            serverRight=serverRight+clientRight
            if serverRight==6:
                serverRight=1
            elif serverRight==7:
                serverRight=2
            elif serverRight==8:
                serverRight=3
            elif serverRight==9:
                serverRight=4
        elif message=="R to L":
            if clientRight==0:
                fingers=False
                while (fingers==False):
                    message=input(str("You cannot attack with a hand that has 0 fingers. Enter your move: "))
                    if (message!="R to R" and message!="R to L"):
                        fingers=True
            serverLeft=serverLeft+clientRight
            if serverLeft==6:
                serverLeft=1
            elif serverLeft==7:
                serverLeft=2
            elif serverLeft==8:
                serverLeft=3
            elif serverLeft==9:
                serverLeft=4
        msg=msg.encode()
        s.send(msg)
        #Enemy Entries
        enemyLText="Enemy left fingers:"
        enemyLLabel=Label(root, text=enemyLText)
        enemyLLabel.grid(row=1, column=1)
        enemyLEntry=Entry(root)
        enemyLEntry.insert(0, serverLeft)
        enemyLEntry.grid(row=1, column=2)
        enemyRText="Enemy right fingers:"
        enemyRLabel=Label(root, text=enemyRText)
        enemyRLabel.grid(row=1, column=3)        
        enemyREntry=Entry(root)
        enemyREntry.insert(0, serverRight)
        enemyREntry.grid(row=1, column=4)
        #Your Entries
        yourLText="Your left fingers:"
        yourLLabel=Label(root, text=yourLText)
        yourLLabel.grid(row=2, column=1)
        yourLEntry=Entry(root)
        yourLEntry.insert(0, clientLeft)
        yourLEntry.grid(row=2, column=2)
        yourRText="Your right fingers:"
        yourRLabel=Label(root, text=yourRText)
        yourRLabel.grid(row=2, column=3)
        yourREntry=Entry(root)
        yourREntry.insert(0, clientRight)
        yourREntry.grid(row=2, column=4)
        
    answer=tkinter.messagebox.askquestion("Finger Chess", "Are you the host?")
    
    if answer=="yes": #server code
        conButton=Button(root, text='Connect', command=serverConn)
        conButton.grid(row=4, column=1, sticky=W, pady=4)
    
    else: #client code
        cliButton=Button(root, text='Connect', command=clientConn).grid(row=4, column=2, pady=4)
        cliLabel1=Label(root, text = "The hostname is:").grid(row=2)
        cliLabel2=Label(root, text="Press the button and connect").grid(row=3)
        hostEntry=Entry(root)
        Ans=socket.gethostname()
        hostEntry.insert(0, Ans)
        hostEntry.grid(row=2, column=1)
        messageCMove = tkinter.StringVar()  # For the messages to be sent.
        messageCMove.set("Type your move here.")
    
    root.mainloop()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

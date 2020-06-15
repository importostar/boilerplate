---
title: Arduino PythonCon
date: 2020-05-07
---
Example Python program Arduino-PythonCon.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import smtplib
* import datetime
* from tkinter import *
* import tkinter 
* import serial, time,os

## Methods

* def send_email(recipient, subject, body):
* def dateS():
* def timeS():
* def change_dropdown(*arg):
* def Start():
* def Stop():

## Code

Python tkinter example

    
    
    def send_email(recipient, subject, body):
    
        import smtplib
    
        user='rXXXXX'
    
        pwd='XXXXX'
    
        FROM = user
    
        TO = recipient if isinstance(recipient, list) else [recipient]
    
        SUBJECT = subject
    
        TEXT = body
    
        # Prepare actual message
    
        message = """From: %s\nTo: %s\nSubject: %s\n\n%s
    
        """ % (FROM, ", ".join(TO), SUBJECT, TEXT)
    
        try:
    
            server = smtplib.SMTP("smtp.gmail.com", 587)
    
            server.ehlo()
    
            server.starttls()
    
            server.login(user, pwd)
    
            server.sendmail(FROM, TO, message)
    
            server.close()
    
            print ('successfully sent the mail')
    
        except:
    
            print ("failed to send mail")
    
            
    
    import datetime
    
    def dateS():
    
        return datetime.datetime.now().strftime('%Y-%m-%d')
    
    def timeS():
    
        return datetime.datetime.now().strftime('%H:%M:%S')
    
    ​
    
    global arduino
    
    
    from tkinter import *
    
    import tkinter 
    
    import serial, time,os
    
    
    root = Tk()
    
    root.title("Refueling Prototype Demo")
    
    root.resizable(False, False) 
    
    # Add a grid
    
    mainframe = Frame(root)
    
    mainframe.grid(column=0,row=0, sticky=(N,W,E,S) )
    
    mainframe.columnconfigure(0, weight = 1)
    
    mainframe.rowconfigure(0, weight = 1)
    
    mainframe.pack(pady = 120, padx = 100)
    
     
    
    # Create a tkinter variable
    
    tkvar = StringVar(root)
    
    
    # Dictionary with options
    
    choices = { '/dev/ttyACM0','/dev/ttyACM1','/dev/ttyACM2','/dev/ttyACM3','/dev/ttyACM4'}
    
    tkvar.set('/dev/ttyACM0') # set the default option
    
     
    
    popupMenu = OptionMenu(mainframe, tkvar, *choices)
    
    Label(mainframe, text="Choose a Port").grid(row = 1, column = 1)
    
    popupMenu.grid(row = 2, column =1)
    
    
    # on change dropdown value
    
    def change_dropdown(*arg):
    
        global arduino
    
        if tkvar.get()=='/dev/ttyACM0':
    
            arduino = os.popen( "sudo aimsadmin /dev/ttyACM0", "r")  # send terminal commande with root permission and save the resulte in "arduino"
    
            arduino = serial.Serial(tkvar.get(), 9600, timeout=.1)
    
            print("Port is open")  
    
            time.sleep(1) #give the connection a second to settle
    
        if tkvar.get()=='/dev/ttyACM1':
    
            arduino = os.popen( "sudo aimsadmin /dev/ttyACM1", "r")
    
            arduino = serial.Serial(tkvar.get(), 9600, timeout=.1)
    
            print("Port is open")
    
            time.sleep(1) 
    
        if tkvar.get()=='/dev/ttyACM2':
    
            arduino = os.popen( "sudo aimsadmin /dev/ttyACM2", "r")
    
            arduino = serial.Serial(tkvar.get(), 9600, timeout=.1)
    
            print("Port is open")
    
            time.sleep(1) 
    
        if tkvar.get()=='/dev/ttyACM3':
    
            arduino = os.popen( "sudo aimsadmin /dev/ttyACM3", "r")
    
            arduino = serial.Serial(tkvar.get(), 9600, timeout=.1)
    
            print("Port is open")
    
            time.sleep(1) 
    
        if tkvar.get()=='/dev/ttyACM4':
    
            arduino = os.popen( "sudo aimsadmin /dev/ttyACM4", "r")
    
            arduino = serial.Serial(tkvar.get(), 9600, timeout=.1)
    
            print("Port is open")
    
            time.sleep(1) 
    
        time.sleep(3)   
    
        return arduino.readline()
    
        
    
     
    
    # link function to change dropdown
    
    tkvar.trace('w', change_dropdown)
    
    
    def Start():
    
        global tvalue   
    
        data = change_dropdown()
    
        if data:
    
            if data==b'Alert!!!\r\n':
    
                print("Alert!!!")
    
                var.set('Click Start Again!!!')
    
            else:
    
                if data==b'Used\r\n':
    
                    var.set('Click Start Again!!!')
    
                else:
    
                    tvalue=float(data)   
    
                    print (tvalue) #strip out the new lines for now
    
                    var.set('Proceed with the Refueling') 
    
                    #return startvalue
    
        else:
    
            print("Empty")
    
            var.set('Click Start Again!!!')
    
            
    
    def Stop():
    
        global tvalue
    
        data = arduino.readline()
    
        if data:
    
            if data==b'Alert!!!\r\n':
    
                print("Alert!!!")
    
                var.set('Click Stop Again!!!')
    
            else:
    
                if data==b'Used\r\n':
    
                    var.set('Click Stop Again!!!')
    
                else:
    
                    stopvalue=float(data)   
    
                    value=stopvalue-tvalue
    
                    print (value) #strip out the new lines for now
    
                    send_email('xxxx','Fueling Operation','Prototype'+'\n'+str(value)+'\n'+dateS()+'\n'+timeS())
    
                    var.set('Refueling Completed')   
    
        else:
    
            print("Empty")
    
            var.set('Click Stop Again!!!')        
    
    #start button    
    
    B = tkinter.Button(root, text ="Start", command = Start, height='3',width='6', font='Cambria', bg='blue',relief=RAISED)
    
    B.pack() 
    
    B.place(x=15, y=200)
    
    ​
    
    #stop button
    
    B1 = tkinter.Button(root, text ="Stop", command = Stop, height='3',width='6', font='Cambria', bg='Red',relief=RAISED)
    
    B1.pack() 
    
    B1.place(x=230, y=200)
    
    
    # Label
    
    var = StringVar()
    
    label = Label( root, textvariable=var, relief=RAISED )
    
    label.pack()
    
    label.place(x=100, y=50)
    
    
    root.mainloop()

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
